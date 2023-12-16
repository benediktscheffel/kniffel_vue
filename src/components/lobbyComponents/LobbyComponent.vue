<template>
  <q-page class="q-pa-md">
    <lobby-form-component
      :yourName="yourName"
      :isJoinButtonDisabled="isJoinButtonDisabled"
      @connectWebSocket="connectWebSocket"
      @updateYourName="updateYourName"
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
      countdown: 60,
      ready: false,
      yourName: '',
      dialogVisible: false,
      leaveDialogVisible: false,
    };
  },
  computed: {
    isJoinButtonDisabled() {
      return this.yourName.trim() === '';
    },
  },
  methods: {
    readyFunction() {
      this.ready = true;
      this.websocket.send(JSON.stringify({event: "ready", playerID: this.playerID}));
    },
    connectWebSocket(playerName) {
      // Your existing WebSocket connection logic
    },
    closeConnection() {
      this.closeSocketConnection().then(() => {
        if (this.ready) {
          this.ready = false;
        }
      });
    },
    async closeSocketConnection() {
      // Your existing closeSocketConnection logic
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
    updateYourName(playerName) {
      this.yourName = playerName;
      if (playerName !== undefined && playerName.length > 0) {
        this.isJoinButtonDisabled = false;
      }
    }
  },
};
</script>

<style>
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
