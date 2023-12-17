<template>
  <q-dialog :model-value="dialogVisible" persistent @update:model-value="updateConfirmationDialog"
            data-bs-backdrop="static">
    <q-card>
      <q-card-section>
        <div class="container centering-block">
          <div class="loader centered">
            <!-- Your loader animation here -->
          </div>
        </div>
        <div>
          <p>
            <span>{{ playersReady }}</span>/<span>{{ playersCount }}</span>
            Players ready
          </p>
          <p>
            <span>Seconds until Start: </span><span>{{ countdown }}</span>
          </p>
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
          <span class="material-symbols-outlined">
          <q-icon v-if="ready">check</q-icon>
          </span>
          Ready
        </q-btn>
        <q-btn flat color="dark" id="leaveLobby" @click="openLeaveDialog">
          Leave
          <span class="material-symbols-outlined">
          <q-icon>exit_to_app</q-icon>
          </span>
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
    countdown: String,
    ready: Boolean,
  },
  methods: {
    readyFunction() {
      this.$emit('readyFunction');
    },
    openLeaveDialog() {
      this.$emit('openLeaveDialog');
    },
    updateConfirmationDialog() {
      this.$emit('updateConfirmationDialog');
    }
  },
};
</script>

<style scoped>
/* Your component-specific styles here */
</style>
