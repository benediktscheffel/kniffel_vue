<template>
  <q-page class="q-pa-md">
    <lobby-form-component
      :isJoinButtonDisabled="isJoinButtonDisabled"
      @connectWebSocket="connectWebSocket"
    />
    <lobby-dialog-component
      :dialogVisible="dialogVisible"
      :playersReady="playersReady"
      :playersCount="playersCount"
      :countdown="countdown"
      :ready="ready"
      @readyFunction="readyFunction"
      @openLeaveDialog="openLeaveDialog"
    />

    <lobby-leave-dialog-component
      :leaveDialogVisible="leaveDialogVisible"
      @leaveLobby="leaveLobby"
      @closeLeaveDialog="closeLeaveDialog"
    />
  </q-page>
</template>

<script>
import LobbyFormComponent from "components/lobbyComponents/LobbyFormComponent.vue";
import LobbyDialogComponent from "components/lobbyComponents/LobbyDialogComponent.vue";
import LobbyLeaveDialogComponent from "components/lobbyComponents/LobbyLeaveDialogComponent.vue";

export default {
  components: {
    LobbyFormComponent,
    LobbyDialogComponent,
    LobbyLeaveDialogComponent,
  },
  data() {
    return {
      playerID: 0,
      timestamp: 0,
      websocket: undefined,
      playersCount: 0,
      playersReady: 0,
      countdown: '60',
      ready: false,
      playerName: '',
      dialogVisible: false,
      leaveDialogVisible: false,
      isJoinButtonDisabled: true,
      gameStarted: false
    };
  },
  methods: {
    readyFunction() {
      this.ready = true;
      this.websocket.send(JSON.stringify({event: "ready", playerID: this.playerID}));
    },
    connectWebSocket(playerName) {
      this.dialogVisible = true;
      this.websocket = new WebSocket("ws://85.215.67.144:9000/lobbyWebsocket");
      this.playerName = playerName
      this.websocket.onopen = () => {
        this.websocket.send(JSON.stringify({event: "newPlayer", name: playerName}));
        console.log("Connected to Websocket");
      }

      this.websocket.onclose = function () {
        console.log('Connection with Websocket Closed!');
      };

      this.websocket.onerror = function (error) {
        console.log('Error in Websocket occurred: ' + error);
      };

      this.websocket.onmessage = (e) => {
        const data = JSON.parse(e.data);
        if (data.event === "updateTimeMessageEvent") {
          this.countdown = (60 - Math.floor(data.time / 1000)).toString()
          this.playersCount = data.numberOfPlayers;
          if (!this.gameStarted && ((data.readyCount === this.playersCount && this.playersCount > 1) || data.startGame)) {
            this.gameStarted = true;
            this.websocket.send(JSON.stringify({
              event: "startGame",
              name: this.playerName,
              playerID: this.playerID
            }));
          }
        } else if (data.event === "newPlayerMessageEvent") {
          this.playerID = data.id;
          this.timestamp = data.timestamp;
          this.playersCount = data.numberOfPlayers;
          this.playersReady = data.readyCount
        } else if (data.event === "readyMessageEvent") {
          this.playersReady = data.readyCount
        } else if (data.event === "closeConnectionMessageEvent") {
          this.closeConfirmationDialog()
        } else if (data.event === "newGameMessageEvent") {
          const playerData = {'id': this.playerID, 'name': this.playerName, 'timestamp': this.timestamp};
          this.setPlayerInSessionStorage(playerData, () => {
            if (data.isInitiator) {
              fetch('http://85.215.67.144:9000/new?players=' + data.players).then(() => {
                this.$router.push("/kniffel");
              });
            } else {
              this.$router.push("/kniffel");
            }
          });
        }
      };
    },
    closeConnection() {
      this.closeSocketConnection().then(() => {
        if (this.ready) {
          this.ready = false;
        }
      });
    },
    async closeSocketConnection() {
      return new Promise((resolve, reject) => {
        this.websocket.send(JSON.stringify({
          event: "closeConnection",
          ready: this.ready,
          playerID: this.playerID
        }));

        function handleMessage(event) {
          const response = JSON.parse(event.data);
          resolve(response);
        }

        this.websocket.addEventListener('message', handleMessage);
      });
    },
    leaveLobby() {
      this.websocket.send(
        JSON.stringify({
          event: 'closeConnection',
          playerID: this.playerID,
          ready: this.ready,
        })
      );
      this.closeLeaveDialog();
      this.closeConfirmationDialog();
    },
    openLeaveDialog() {
      this.leaveDialogVisible = true;
    },
    closeLeaveDialog() {
      this.leaveDialogVisible = false;

    },
    updateLeaveLobbyDialog() {
      this.leaveDialogVisible = !this.leaveDialogVisible
    },
    updateConfirmationDialog() {
      this.dialogVisible = !this.dialogVisible
    },
    closeConfirmationDialog() {
      this.dialogVisible = false;
    },
    setPlayerInSessionStorage(player, callback) {
      sessionStorage['player'] = JSON.stringify(player);
      if (sessionStorage['player'] === JSON.stringify(player)) {
        callback();
      } else {
        setTimeout(() => {
          console.log("Failed setting player %o in sessionStorage! Retrying...", player);
          this.setPlayerInSessionStorage(callback);
        }, 1000);
      }
    },
  },
};
</script>

<style scoped>
main {
  display: flex;
  align-items: center;
}
q-card-section {
  position: relative;
  background-color: #fefefe;
  margin: auto;
  padding: 0;
  border-radius: 15px;
  width: 70%;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  -webkit-animation-name: animatetop;
  -webkit-animation-duration: 0.4s;
  animation-name: animatetop;
  animation-duration: 0.4s
}

q-card {
  display: none;
  position: fixed;
  padding-top: 40vh;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background-color: rgb(0, 0, 0);
  background-color: rgba(0, 0, 0, 0.4);
}

q-card-actions {
  padding-top: 5px;
  padding-bottom: 5px;
  background-color: #9f4045;
}
</style>
