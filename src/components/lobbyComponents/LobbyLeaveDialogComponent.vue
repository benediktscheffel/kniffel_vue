<template>
  <q-dialog :model-value="leaveDialogVisible" persistent @update:model-value="updateLeaveLobbyDialog">
    <q-card>
      <q-card-section>
        Are you sure you want to leave?
      </q-card-section>

      <q-card-actions align="center">
        <q-btn flat color="dark" @click="leaveLobby">Yes</q-btn>
        <q-btn flat color="dark" @click="closeLeaveDialog">No</q-btn>
      </q-card-actions>
    </q-card>
  </q-dialog>
</template>

<script>
export default {
  props: {
    leaveDialogVisible: Boolean,
  },
  methods: {
    leaveLobby() {
      this.$emit('leaveLobby');
      this.closeLeaveDialog();
    },
    updateLeaveLobbyDialog() {
      this.$emit('updateLeaveLobbyDialog')
    },
    closeLeaveDialog() {
      this.$emit('closeLeaveDialog');
    },
  },
};
</script>

<style scoped>

</style>
