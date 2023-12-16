<template>
  <q-dialog v-model="confirmationDialog" persistent>
    <q-card>
      <q-card-section class="q-pt-none">
      </q-card-section>

      <q-card-section class="q-pt-none">
        <div class="q-pa-md q-gutter-sm">
          <div class="q-mb-md text-h6">Players ready: {{ playersReady }}/{{ playersCount }} Players ready</div>
          <div class="q-mb-md">Seconds until Start: {{ countdown }}</div>
        </div>

        <q-card-actions align="right">
          <q-btn
            flat
            @click="readyFunction"
            :disable="ready"
            :color="ready ? 'green' : 'dark'"
          >
            <q-icon v-if="ready" name="check" class="q-mr-sm"/>
            Ready
          </q-btn>
          <q-btn flat @click="openConfirmationDialog" color="dark">
            Leave
            <q-icon name="exit_to_app" class="q-ml-sm"/>
          </q-btn>
        </q-card-actions>
      </q-card-section>
    </q-card>
  </q-dialog>

  <q-dialog v-model="leaveLobbyConfirmationDialog" persistent>
    <q-card>
      <q-card-section class="q-pt-none">
      </q-card-section>

      <q-card-section class="q-pt-none">
        <q-card-actions align="right">
          <q-btn flat @click="leaveLobby" color="dark">Yes</q-btn>
          <q-btn flat @click="leaveLobbyConfirmationDialog = false" color="dark">No</q-btn>
        </q-card-actions>
      </q-card-section>
    </q-card>
  </q-dialog>
</template>

<script>
export default {
  data() {
    return {
      playerID: 0,
      timestamp: 0,
      websocket: undefined,
      playersCount: 0,
      playersReady: 0,
      countdown: 60,
      ready: false,
      yourName: ''
    }
  },
  methods: {
    readyFunction() {
      this.ready = true;
      this.websocket.send(JSON.stringify({event: "ready", playerID: this.playerID}));
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
    connectWebSocket(playerName) {
      const countdown = document.getElementById("countdown");
      this.websocket = new WebSocket("ws://localhost:9000/lobbyWebsocket");
      this.playerName = playerName
      this.websocket.onopen = (event) => {
        this.websocket.send(JSON.stringify({event: "newPlayer", name: playerName}));
        /*$.ajax({
            method: "GET", url: '/isRunning',
            success: function (data) {
              if (data.isRunning) {
                  websocket.send(JSON.stringify({"event": "clearAll"}));
              }
            }
        });*/
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
          if ((data.readyCount === this.playersCount && this.playersCount > 1) || data.startGame) {
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
          $('#confirmationDialog').modal('hide');
        } else if (data.event === "newGameMessageEvent") {
          const playerData = {'id': this.playerID, 'name': this.playerName, 'timestamp': this.timestamp};
          this.setPlayerInSessionStorage(playerData, () => {
            if (data.isInitiator) {
              fetch('/new?players=' + data.players).then(() => {
                window.location.href = '/kniffel'
              });
              /*  $.ajax({
                    method: "GET", url: '/new?players=' + data.players,
                    success: function () {
                        window.location.href = '/kniffel';
                    },
                    error: function(jqXHR, textStatus, errorThrown) {
                        console.error("Failed starting new game!");
                    }
                });*/
            } else {
              window.location.href = '/kniffel';
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
      })
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
      this.websocket.send(JSON.stringify({event: "closeConnection", playerID: this.playerID, ready: this.ready}));
    },
    openConfirmationDialog() {
      $('#leaveLobbyConfirmationDialog').modal('show')
    }
  }
};
</script>
