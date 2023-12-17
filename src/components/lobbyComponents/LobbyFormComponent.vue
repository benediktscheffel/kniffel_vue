<template>
  <div class="col">
    <q-img style="display: block; margin: auto" src="src/assets/images/flying_dices_small.png"/>
    <h1 style="text-align: center">Welcome to Kniffel</h1>
    <h3 style="text-align: center; margin-bottom: 20px">Let the dice roll</h3>
    <q-form>
      <q-input
        v-model="yourName"
        filled
        outlined
        id="yourName"
        class="yourNameLabel"
        label="Your Name"
      ></q-input>
      <q-btn
        :disable="yourName.length === 0"
        type="button"
        data-bs-toggle="modal"
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
  display: flex;
  justify-content: center;
  align-items: center;
}

.yourNameLabel {
  font-weight: bold;
  font-size: 16px;
  margin-bottom: 0;
}

#yourName {
  width: 160px;
  height: 30px;
  font-size: 16px;
  margin: 0 10px;
  text-align: center;
  border-radius: 15px;
}

@-webkit-keyframes animatetop {
  from {
    top: -300px;
    opacity: 0
  }
  to {
    top: 0;
    opacity: 1
  }
}

@keyframes animatetop {
  from {
    top: -300px;
    opacity: 0
  }
  to {
    top: 0;
    opacity: 1
  }
}

.close {
  color: white;
  float: right;
  font-size: 28px;
  font-weight: bold;
}

.close:hover,
.close:focus {
  color: #000;
  text-decoration: none;
  cursor: pointer;
}

.modal-header {
  padding: 2px 16px;
  text-align: center !important;
  background-color: #9f4045;
  border-radius: 10px 10px 0 0;
  color: white;
}

.modal-body {
  text-align: center;
  font-size: large;
  color: black;
  background-color: white;
  display: flex;
  flex-direction: row;
}

#ready {
  width: 75px;
}

.container {
  height: 100%;
}

.centering-block {
  text-align: center;
  width: 100px;
  -webkit-transform: translateZ(0) scale(0.8);
  -moz-transform: translateZ(0) scale(0.8);
  transform: translateZ(0) scale(0.8);
  margin: 0;
  padding: 0;
}

.centering-block:before {
  content: '';
  display: inline-block;
  box-sizing: unset;
  height: 100%;
  vertical-align: middle;
  margin-right: -0.25em;
}

.centered {
  vertical-align: middle;
  width: 69px !important;
}

.loader {
  display: inline-block;
  position: relative;
  width: 80px;
  animation: roll_dice 2.22s infinite ease-in;
}

.loader .square {
  background-color: lightgrey;
  width: 20px;
  height: 20px;
  display: inline-block;
  opacity: 1;
  transition: background-color 0.25s;
}

.loader .animationRow {
  width: 68px;
  display: flex;
  padding: 1.5px 0;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: space-around;
}

.loader .square_one {
  animation: square_one 10s infinite;
}

.loader .square_two {
  animation: square_two 10s infinite;
}

.loader .square_three {
  animation: square_three 10s infinite;
}

.loader .square_four {
  animation: square_four 10s infinite;
}

.loader .square_five {
  animation: square_five 10s infinite;
}

.loader .square_six {
  animation: square_six 10s infinite;
}

.loader .square_seven {
  animation: square_seven 10s infinite;
}

.loader .square_eight {
  animation: square_eight 10s infinite;
}

.loader .square_nine {
  animation: square_nine 10s infinite;
}

@keyframes roll_dice {
  0% {
    transform: rotate(0deg);
  }

  25% {
    transform: rotate(180deg);
  }

  50% {
    transform: rotate(180deg);
  }

  75% {
    transform: rotate(360deg);
  }

  100% {
    transform: rotate(360deg);
  }
}

@keyframes square_one {
  0% {
    background-color: lightgrey;
  }
  12.5% {
    background-color: lightgrey;
  }
  25% {
    background-color: rgba(var(--bs-dark-rgb));
  }
  37.5% {
    background-color: lightgrey;
  }
  50% {
    background-color: rgba(var(--bs-dark-rgb));
  }
  62.5% {
    background-color: rgba(var(--bs-dark-rgb));
  }
  75% {
    background-color: rgba(var(--bs-dark-rgb));
  }
  87.5% {
    background-color: #f2ece4;
  }
  100% {
    background-color: lightgrey;
  }
}

@keyframes square_two {
  0% {
    background-color: lightgrey;
  }
  12.5% {
    background-color: lightgrey;
  }
  25% {
    background-color: lightgrey;
  }
  37.5% {
    background-color: lightgrey;
  }
  50% {
    background-color: lightgrey;
  }
  62.5% {
    background-color: lightgrey;
  }
  75% {
    background-color: lightgrey;
  }
  87.5% {
    background-color: #f2ece4;
  }
  100% {
    background-color: lightgrey;
  }
}

@keyframes square_three {
  0% {
    background-color: lightgrey;
  }
  12.5% {
    background-color: lightgrey;
  }
  25% {
    background-color: lightgrey;
  }
  37.5% {
    background-color: rgba(var(--bs-dark-rgb));
  }
  50% {
    background-color: rgba(var(--bs-dark-rgb));
  }
  62.5% {
    background-color: rgba(var(--bs-dark-rgb));
  }
  75% {
    background-color: rgba(var(--bs-dark-rgb));
  }
  87.5% {
    background-color: #f2ece4;
  }
  100% {
    background-color: lightgrey;
  }
}

@keyframes square_four {
  0% {
    background-color: lightgrey;
  }
  12.5% {
    background-color: lightgrey;
  }
  25% {
    background-color: lightgrey;
  }
  32.5% {
    background-color: lightgrey;
  }
  50% {
    background-color: lightgrey;
  }
  62.5% {
    background-color: lightgrey;
  }
  75% {
    background-color: rgba(var(--bs-dark-rgb));
  }
  87.5% {
    background-color: #f2ece4;
  }
  100% {
    background-color: lightgrey;
  }
}

@keyframes square_five {
  0% {
    background-color: lightgrey;
  }
  12.5% {
    background-color: rgba(var(--bs-dark-rgb));
  }
  25% {
    background-color: lightgrey;
  }
  37.5% {
    background-color: rgba(var(--bs-dark-rgb));
  }
  50% {
    background-color: lightgrey;
  }
  62.5% {
    background-color: rgba(var(--bs-dark-rgb));
  }
  75% {
    background-color: lightgrey;
  }
  87.5% {
    background-color: #f2ece4;
  }
  100% {
    background-color: lightgrey;
  }
}

@keyframes square_six {
  0% {
    background-color: lightgrey;
  }
  12.5% {
    background-color: lightgrey;
  }
  25% {
    background-color: lightgrey;
  }
  37.5% {
    background-color: lightgrey;
  }
  50% {
    background-color: lightgrey;
  }
  62.5% {
    background-color: lightgrey;
  }
  75% {
    background-color: rgba(var(--bs-dark-rgb));
  }
  87.5% {
    background-color: #f2ece4;
  }
  100% {
    background-color: lightgrey;
  }
}

@keyframes square_seven {
  0% {
    background-color: lightgrey;
  }
  12.5% {
    background-color: lightgrey;
  }
  25% {
    background-color: lightgrey;
  }
  37.5% {
    background-color: rgba(var(--bs-dark-rgb));
  }
  50% {
    background-color: rgba(var(--bs-dark-rgb));
  }
  62.5% {
    background-color: rgba(var(--bs-dark-rgb));
  }
  75% {
    background-color: rgba(var(--bs-dark-rgb));
  }
  87.5% {
    background-color: #f2ece4;
  }
  100% {
    background-color: lightgrey;
  }
}

@keyframes square_eight {
  0% {
    background-color: lightgrey;
  }
  12.5% {
    background-color: lightgrey;
  }
  25% {
    background-color: lightgrey;
  }
  37.5% {
    background-color: lightgrey;
  }
  50% {
    background-color: lightgrey;
  }
  62.5% {
    background-color: lightgrey;
  }
  75% {
    background-color: lightgrey;
  }
  87.5% {
    background-color: #f2ece4;
  }
  100% {
    background-color: lightgrey;
  }
}

@keyframes square_nine {
  0% {
    background-color: lightgrey;
  }
  12.5% {
    background-color: lightgrey;
  }
  25% {
    background-color: rgba(var(--bs-dark-rgb));
  }
  37.5% {
    background-color: lightgrey;
  }
  50% {
    background-color: rgba(var(--bs-dark-rgb));
  }
  62.5% {
    background-color: rgba(var(--bs-dark-rgb));
  }
  75% {
    background-color: rgba(var(--bs-dark-rgb));
  }
  87.5% {
    background-color: #f2ece4;
  }
  100% {
    background-color: lightgrey;
  }
}
</style>
