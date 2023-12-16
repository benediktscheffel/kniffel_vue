<template>
  <q-page class="q-pa-md">
    <lobby-form-component
      :yourName="yourName"
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
    }
  },
};
</script>

<style scoped>
/* Your component-specific styles here */
</style>
