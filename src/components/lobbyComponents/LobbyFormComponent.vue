<template>
  <div class="startGame col">
    <q-img id="img" style="display: block; margin: auto" src="src/assets/images/flying_dices.png"/>
    <h1 style="text-align: center">Welcome to Kniffel</h1>
    <h3 style="text-align: center; margin-bottom: 20px">Let the dice roll</h3>
    <q-form>
      <q-input v-model="yourName" filled outlined class="yourNameLabel" label="Your Name"></q-input>
      <q-btn :disable="yourName.length === 0" class="startButton" color="dark" @click="connectWebSocket(yourName)">
        Join
      </q-btn>
    </q-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      yourName: '',
    }
  },
  props: {
    isJoinButtonDisabled: Boolean,
  },
  methods: {
    connectWebSocket(playerName) {
      this.$emit('connectWebSocket', playerName);
    },
  },
};
</script>
<style scoped>
.startGame {
  height: 90vh;
  width: 70vh;
  display: compact;

  justify-content: center;
  align-items: center;
}

.yourNameLabel {
  font-weight: bold;
  font-size: 16px;
  margin-bottom: 0;
}

q-img {
  display: flex;
  width: 10vh;
  height: 5%;
}

h1, h3 {
  font-size: 40px;
}

#img {
  max-height: 120px;
  max-width: 120px;
}
</style>
