<template>
  <q-page class="q-pa-md">
    <q-container class="q-pa-md">
      <q-row align="center" justify="center">
        <q-col>
          <LobbyFormComponent
            :yourName="yourName"
            :isJoinButtonDisabled="isJoinButtonDisabled"
            @connectWebSocket="connectWebSocket"
          />
        </q-col>
      </q-row>
    </q-container>

    <LobbyDialogComponent
      :dialogVisible="dialogVisible"
      :playersReady="playersReady"
      :playersCount="playersCount"
      :countdown="countdown"
      :ready="ready"
      @readyFunction="readyFunction"
      @openLeaveDialog="openLeaveDialog"
    />

    <LobbyLeaveDialogComponent
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
  },
};
</script>

<style scoped>
/* Your component-specific styles here */
</style>
