<script>
export default {
  props: {
    remainingDices: Number,
    active: Boolean,
  },
  methods: {
    putAllIn() {
      this.$emit('putAllIn')
    },
    dice() {
      this.$emit('dice')
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

    <q-btn type="button" style="margin-top: 5px" id="allInButton" class="q-ml-md" color="dark" @click="putAllIn"
           :disable="!active || remainingDices < 0"
    >
      <span class="material-symbols-outlined">
        <q-icon name="keyboard_double_arrow_left"/>
      </span>
    </q-btn>

    <q-btn style="margin-top: 5px;" class="q-ml-md" color="dark" @click="dice" :disable="remainingDices < 0 || !active">
      <span class="material-symbols-outlined">
        <q-img src="src/assets/images/flying_dices_small_white.png" style="margin-top: -12px;" width="40px"/>
      </span>
    </q-btn>
  </div>
</template>

<style scoped>

.actionBox {
  justify-content: center;
  align-content: center;
  display: flex;
  //flex-direction: column;
  margin-left: 30px;
  margin-bottom: 7px;
  margin-top: 7px;
}

.action-box {
  width: 55%;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.q-btn {
  min-height: 35px;
  height: 35px;
  width: 80px;
  font-size: 1.2em;
}

.q-btn .q-icon, .q-btn .q-spinner {
  font-size: unset;
  vertical-align: baseline;
}

.q-ml-md {
  margin-left: 0;
}

</style>
