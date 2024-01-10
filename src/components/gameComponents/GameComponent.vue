<template>
  <div class="gameContainer">
    <dice-cup-component
      :incup="incup"
      :remaining-dices="remainingDices"
      :stored="stored"
      :active="active"
      @putOut="putOut"
      @putIn="putIn"
      @putAllIn="putAllIn "
      @dice="dice"
      style="align-content: center"
    ></dice-cup-component>
    <field-component
      @writeTo="writeTo"
      :current-player="this.currentPlayer"
      :matrix="this.matrix"
      :players="this.players[0]"
      :number-of-players="this.numberOfPlayers"
      :active="this.active"
      :suggestions="this.suggestions"
    ></field-component>
    <chat-component
      @sendChatMessage="sendChatMessage"
      :chatMessages="chatMessages"
      :player-name="playerName"
      @refreshChat="refreshChat"
    ></chat-component>

  </div>
</template>

<script>
import DiceCupComponent from 'components/gameComponents/DiceCupComponent.vue'
import FieldComponent from 'components/gameComponents/FieldComponent.vue'
import ChatComponent from 'components/gameComponents/ChatComponent.vue'
import $ from 'jquery'

export default {
  components: {
    DiceCupComponent,
    FieldComponent,
    ChatComponent
  },
  data() {
    return {
      gameSocket: undefined,
      chatUrl: '',
      incup: [],
      remainingDices: 2,
      stored: [],
      active: false,
      matrix: [],
      players: [],
      numberOfPlayers: 0,
      currentPlayer: 0,
      writeDownMappingsForLowerPart: ['3X', '4X', 'FH', 'KS', 'GS', 'KN', 'CH'],
      chatMessages: [],
      backendUrl: 'http://85.215.67.144:9000',
      playerName: '',
      suggestions: undefined
    }
  },
  created() {
    console.log('HERE')
    this.initGameSocket()
    this.getChatUrl()
    this.getCurrentGameState()
    this.getCurrentField()
  },
  methods: {
    onWebSocketOpen() {
      // diceCup
      $.ajax({
        url: this.backendUrl + '/dicecup',
        type: 'GET',
        success: (data) => {
          this.incup = data.dicecup.incup
          this.remainingDices = data.dicecup.remainingDices
          this.stored = data.dicecup.stored
        },
        error: function () {
          console.error('Failed to get dicecup JSON.')
        }
      })

      // field
      $.ajax({
        url: this.backendUrl + '/field',
        type: 'GET',
        success: (data) => {
          this.matrix = data.controller.field.rows
          this.controller = data.controller
          this.currentPlayer = data.controller.game.currentPlayerID
          this.numberOfPlayers = this.matrix[0].length
          this.players = this.controller.game.players
        }
      })
    },
    initGameSocket() {
      this.gameSocket = new WebSocket('ws://85.215.67.144:9000/websocket')

      this.gameSocket.onopen = (event) => {
        this.waitForPlayer((p) => {
          const player = JSON.parse(p)
          this.playerID = player.id
          this.playerName = player.name
          console.log(this.playerName)
          const timestamp = player.timestamp
          this.onWebSocketOpen()
          this.gameSocket.send(JSON.stringify({
            event: 'playerJoined',
            name: this.playerName,
            id: this.playerID,
            timestamp: timestamp
          }));
          console.log(this.playerID)
          if (this.playerID === 0) {
            this.active = true
          }
        })
        console.log('Connected to Websocket')
      }

      this.gameSocket.onclose = function () {
        console.log('Connection with Websocket Closed!')
      }

      this.gameSocket.onerror = function (error) {
        console.log('Error in Websocket Occured: ' + error)
      }

      this.gameSocket.onmessage = (e) => {
        if (typeof e.data === 'string') {
          if (JSON.parse(e.data).controller !== undefined) {
            this.incup = e.data.incup
            this.stored = e.data.stored
            this.remainingDices = e.data.remainingDices
            this.controller = e.data.controller
            if (this.controller) {
              this.matrix = this.controller.field.rows
              this.currentPlayer = this.controller.game.currentPlayerID
              // this.popoverContent = this.generatePopoverContent();
            }
          } else if (JSON.parse(e.data).dicecup !== undefined) {
            console.log('DiceCup Changed')
            if (JSON.parse(e.data).isDice) {
              this.diceCupAnimationStart();
              this.incup = JSON.parse(e.data).dicecup.incup
              this.remainingDices = JSON.parse(e.data).dicecup.remainingDices
              this.stored = JSON.parse(e.data).dicecup.stored
              this.updateSuggestions()
            } else {
              this.incup = JSON.parse(e.data).dicecup.incup
              this.remainingDices = JSON.parse(e.data).dicecup.remainingDices
              this.stored = JSON.parse(e.data).dicecup.stored
              // buildField();
            }
          } else if (JSON.parse(e.data).field !== undefined) {
            this.matrix = e.data.field.rows
            // this.popoverContent = this.generatePopoverContent();
            // buildField()
            /* console.log("Field Changed") */
          } else if (JSON.parse(e.data).event === 'turnChangedMessageEvent') {
            console.log('playerID: ' + this.playerID + '; currentTurn: ' + JSON.parse(e.data).currentTurn)
            if (this.playerID !== JSON.parse(e.data).currentTurn) {
              this.active = false
              console.log('deactivate')
              // deactivateButtons(true);
            } else {
              this.active = true
              console.log('activate')
            }
            this.remainingDices = 2
            this.getCurrentField()
            this.suggestions = undefined
          } else if (JSON.parse(e.data).event === 'refreshChatsMessageEvent') {
            this.refreshChat()
          } else {
            /* console.log("Other Change") */
          }
        }
      }
    },
    waitForPlayer(callback) {
      const player = sessionStorage['player'];
      if (player) {
        callback(player)
      } else {
        setTimeout(() => {
          console.error('Failed reading player! Retrying...')
          this.waitForPlayer(callback)
        }, 1000)
      }
    },
    sendChatMessage(messageContent) {
      if (this.chatUrl.length === 0) {
        this.getChatUrl()
      }

      // for future authorization
      /* let username = "chatUser";
      let password = "";
      let credentials = username + ":" + password;
      let authToken = "Basic " + btoa(credentials); */

      const myMessage = {author: this.playerName, content: messageContent}
      $.ajax({
        url: this.chatUrl,
        method: 'POST',
        data: JSON.stringify(myMessage),
        success: () => {
          this.gameSocket.send(JSON.stringify({event: 'refreshChats'}))
        },
        error: function (err) {
          console.error('Failed sending message: %o', err)
        }
      })
    },
    refreshChat() {
      $.ajax({
        method: 'GET',
        dataType: 'json',
        url: this.chatUrl,
        success: (data) => {
          this.chatMessages = data.messages
        },
        error: function (err) {
          console.error('Failed reloading messages: %o', err)
        }
      })
    },
    getChatUrl() {
      $.ajax({
        url: this.backendUrl + '/chatid',
        method: 'GET',
        success: (data) => {
          console.log('Success: ' + data)
          this.chatUrl = 'http://85.215.67.144/' + data + '/messages'
        },
        error: () => {
          console.error("Couldn't recieve CHAT-URL from backend")
        }
      })
    },
    putIn(diceValue) {
      $.ajax({
        url: this.backendUrl + '/in',
        type: 'GET',
        data: {
          in: diceValue
        },
        success: (data) => {
          this.incup = data.dicecup.incup
          this.stored = data.dicecup.stored
        },
        error: function () {
          console.error('Failed to get dicecup JSON.')
        }
      })
    },
    putOut(diceValue) {
      $.ajax({
        url: this.backendUrl + '/out',
        type: 'GET',
        data: {
          out: diceValue
        },
        success: (data) => {
          this.incup = data.dicecup.incup
          this.stored = data.dicecup.stored
        },
        error: function () {
          console.error('Failed to get dicecup JSON.')
        }
      })
    },
    putAllIn() {
      $.ajax({
        url: this.backendUrl + '/in/all',
        type: 'GET',
        success: (data) => {
          this.incup = data.dicecup.incup
          this.stored = data.dicecup.stored
        },
        error: function () {
          console.error('Failed to get dicecup JSON.')
        }
      })
    },
    dice() {
      $.ajax({
        url: this.backendUrl + '/dice',
        method: 'GET',
        success: (data) => {
          this.incup = data.dicecup.incup
          this.stored = data.dicecup.stored
          this.remainingDices = data.dicecup.remainingDices
          this.updateSuggestions()
        },
        error: function () {
          console.error('Failed to get dicecup JSON.')
        }
      })

    },
    updateSuggestions() {
      $.ajax({
        url: this.backendUrl + '/suggestions',
        method: 'GET',
        success: (data) => {
          this.suggestions = data
        },
        error: () => {
          console.error('Failed to update suggestions');
        }
      });
    },
    writeTo(row) {
      const index = row < 6 ? (row + 1) : this.writeDownMappingsForLowerPart[row - 9]
      $.ajax({
        url: this.backendUrl + '/write',
        type: 'GET',
        data: {
          to: index
        },
        success: (data) => {
          this.matrix = data.controller.field.rows
          this.controller = data.controller
          this.currentPlayer = data.controller.game.currentPlayerID
          this.numberOfPlayers = this.matrix[0].length
          this.players = this.controller.game.players
          this.gameSocket.send(JSON.stringify({event: 'nextRound'}))
          this.suggestions = undefined
        },
        error: function () {
          console.error('Failed to write down the result!')
        }
      })
    },
    getCurrentGameState() {
      this.getCurrentDiceCup()
      this.getCurrentField()
    },
    getCurrentDiceCup() {
      $.ajax({
        url: this.backendUrl + '/dicecup',
        method: 'GET',
        success: (data) => {
          this.incup = data.dicecup.incup
          this.stored = data.dicecup.stored
          this.remainingDices = data.dicecup.remainingDices
          if (this.remainingDices < 2) {
            this.updateSuggestions()
          }
        }
      })
    },
    getCurrentField() {
      $.ajax({
        url: this.backendUrl + '/field',
        type: 'GET',
        success: (data) => {
          this.matrix = data.controller.field.rows
          this.controller = data.controller
          this.currentPlayer = data.controller.game.currentPlayerID
          this.numberOfPlayers = this.matrix[0].length
          this.players = this.controller.game.players
        }
      })
    },
    waitForAnimationEnd(element) {
      return new Promise(resolve => {
        element.addEventListener('animationend', function handler() {
          element.removeEventListener('animationend', handler);
          resolve();
        });
      });
    },
    diceCupAnimationStart() {
      const animatedElement = document.querySelector('.cup');
      const diceCupAudio = new Audio('src/assets/sounds/dice_sound.mp3');
      animatedElement.addEventListener('animationstart', () => {
        diceCupAudio.play().then();
        for (const die of document.getElementById('diceInCup').children) {
          die.style.visibility = 'hidden';
        }
      });
      animatedElement.style = "animation: 'auto ease 0s 1 normal none running'; background: url('src/assets/images/cup.png')";
      animatedElement.classList.add('showCup');
      this.waitForAnimationEnd(animatedElement).then(() => {
        animatedElement.style.background = 'none';
        animatedElement.style.animation = 'none';
        for (const die of document.getElementById('diceInCup').children) {
          die.style.visibility = 'visible';
        }
      });
    }
  }
}

</script>

<style>
@media screen and (max-width: 350px) {
  .gameContainer {
    width: 120%;
  }
}


.hide {
  display: none;
}

.showCup {
  display: block;
  animation: shake 1s cubic-bezier(0.36, 0.07, 0.19, 0.97) both;
  transform: translate3d(0, 0, 0);
  backface-visibility: hidden;
  perspective: 1000px;
  opacity: 1
}

@keyframes shake {
  10%, 90% {
    transform: translate3d(-4px, -4px, 0)
  }
  20%, 80% {
    transform: translate3d(8px, 8px, 0)
  }
  30%, 50%, 70% {
    transform: translate3d(-16px, -16px, 0)
  }
  40%, 60% {
    transform: translate3d(16px, 16px, 0)
  }
}
</style>
