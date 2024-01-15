<template>
  <div class="startGame col justify-content-center">
    <q-img id="img" style="display: block; margin: auto" src="src/assets/images/flying_dices.png"/>
    <h1 style="text-align: center">Welcome to Kniffel TEEEEEEEEEEEST</h1>
    <h3 style="text-align: center">Let the dice roll</h3>
    <q-form>
      <div class="row row-cols-2 justify-evenly items-center">
        <q-input :label-color="'white'" :input-style="{color: 'white'}" v-model="yourName" filled outlined class="yourNameLabel" label="Your Name"></q-input>
        <q-btn :disable="yourName.length === 0" class="startButton" color="dark" @click="connectWebSocket(yourName)">
          Join
        </q-btn>
      </div>
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

.yourNameLabel {
  font-weight: bold;
  font-size: 16px;
  margin-bottom: 0;
}
.q-field {
  width: 160px;
}

q-img {
  display: flex;
  width: 10vh;
  height: 5%;
}

h1, h3 {
  font-size: 40px;
  line-height: 15px;
}


#img {
  max-height: 120px;
  max-width: 120px;
}

@media screen and (max-width: 600px) {
  .startGame {
    margin-left: 0;
    margin-right: 0;
  }
  h1, h3 {
    font-size: 25px;
    line-height: 30px;
  }
  .q-field {
    width: 120px;
  }
}

@media screen and (max-width: 350px) {
  h1, h3 {
    font-size: 23px;
    line-height: 25px;
  }
}

.startButton {
  width: 80px;
  height: 30px;
}
</style>
