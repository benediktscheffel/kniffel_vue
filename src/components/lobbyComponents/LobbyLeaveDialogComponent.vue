<!-- LeaveDialog.vue -->
<template>
  <q-dialog v-model="leaveDialogVisible" persistent>
    <q-card>
      <q-card-section>
        <q-paragraph>Are you sure you want to leave?</q-paragraph>
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
    closeLeaveDialog() {
      this.$emit('closeLeaveDialog');
    },
  },
};
</script>

<style scoped>
/* Your component-specific styles here */
</style>
