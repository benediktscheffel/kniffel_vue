<!-- LobbyDialog.vue -->
<template>
  <q-dialog v-model="dialogVisible" persistent>
    <q-card>
      <q-card-section>
        <div class="container centering-block">
          <div class="loader centered">
            <!-- Your loader animation here -->
          </div>
        </div>
        <div>
          <q-paragraph>
            <span>{{ playersReady }}</span>/<span>{{ playersCount }}</span>
            Players ready
          </q-paragraph>
          <q-paragraph>
            <span>Seconds until Start: </span><span>{{ countdown }}</span>
          </q-paragraph>
        </div>
      </q-card-section>

      <q-card-actions align="center">
        <q-btn
          flat
          color="dark"
          id="ready"
          @click="readyFunction"
          :style="{ backgroundColor: ready ? 'green' : '', borderColor: ready ? 'green' : '' }"
        >
          <q-icon v-if="ready">check</q-icon>
          Ready
        </q-btn>
        <q-btn flat color="dark" id="leaveLobby" @click="openLeaveDialog">
          Leave
          <q-icon>exit_to_app</q-icon>
        </q-btn>
      </q-card-actions>
    </q-card>
  </q-dialog>
</template>

<script>
export default {
  props: {
    dialogVisible: Boolean,
    playersReady: Number,
    playersCount: Number,
    countdown: Number,
    ready: Boolean,
  },
  methods: {
    readyFunction() {
      this.$emit('readyFunction');
    },
    openLeaveDialog() {
      this.$emit('openLeaveDialog');
    },
  },
};
</script>

<style scoped>
/* Your component-specific styles here */
</style>
