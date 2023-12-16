<!-- LobbyForm.vue -->
<template>
  <div class="col">
    <q-img style="display: block; margin: auto" src="src/assets/images/flying_dices.png"/>
    <h1 style="text-align: center">Welcome to Kniffel</h1>
    <h3 style="text-align: center; margin-bottom: 20px">Let the dice roll</h3>
    <q-form>
      <q-input
        :model-value="yourName"
        filled
        outlined
        label="Your Name"
        placeholder="Your Name here"
        @update:model-value="updateYourName"
      ></q-input>
      <q-btn
        :disable="isJoinButtonDisabled"
        type="button"
        data-bs-toggle="modal"
        data-bs-target="#confirmationDialog"
        class="startButton"
        color="dark"
        @click="connectWebSocket(yourName)"
      >
        Join
      </q-btn>
    </q-form>
  </div>
</template>

<script>
export default {
  props: {
    yourName: String,
    isJoinButtonDisabled: Boolean,
  },
  methods: {
    connectWebSocket(playerName) {
      this.$emit('connectWebSocket', playerName);
    },
    updateYourName() {
      if (this.yourName !== undefined && this.yourName.length !== 0) {
        this.isJoinButtonDisabled = true
      }
    },
  },
};
</script>
<style scoped>
/* Your component-specific styles here */
</style>
