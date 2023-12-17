<script>
export default {
  props: {
    remainingDices: Number,
    active: Boolean,
  },
  methods: {
    putAllIn() {
      // Emit an event or perform logic
    },
    dice() {
      // Emit an event or perform logic
    },
  },
};
</script>

<template>
  <div class="action-box">
    <q-img src="src/assets/images/dicecup_small.png" id="remDice3" :style="{
      opacity: remainingDices < 2 ? 0.3 : 1
    }"/>

    <q-img src="src/assets/images/dicecup_small.png" id="remDice2" :style="{
      opacity: remainingDices < 1 ? 0.3 : 1
    }"/>

    <q-img src="src/assets/images/dicecup_small.png" id="remDice1" :style="{
      opacity: remainingDices < 0 ? 0.3 : 1
    }"/>

    <q-btn
      type="button"
      style="margin-top: 5px"
      id="allInButton"
      class="q-ml-md"
      color="dark"
      @click="putAllIn"
      :disable="!active"
    >
      <q-icon name="keyboard_double_arrow_left"/>
    </q-btn>

    <q-btn
      type="button"
      style="margin-top: 5px;"
      id="diceButton"
      class="q-ml-md"
      color="dark"
      @click="dice"
      :disable="remainingDices < 0 || !active"
    >
      <q-img src="src/assets/images/flying_dices_small_white.png" style="margin-top: -5px;" width="40px"/>
    </q-btn>
  </div>
</template>

<style scoped>
.actionBox {
  display: flex;
  flex-direction: column;
  margin-left: 30px;
}

.actionBox img {
  width: 50%;
  text-align: center;
  margin: auto;
}
</style>
