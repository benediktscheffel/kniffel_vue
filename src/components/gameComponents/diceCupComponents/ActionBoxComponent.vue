<script>
import DiceCupActionButtonComponent from 'components/gameComponents/diceCupComponents/DiceCupActionButtonComponent.vue';
export default {
  components: {
    DiceCupActionButtonComponent
  },
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
    <dice-cup-action-button-component @putAllIn="putAllIn" :disabled="!active || remainingDices < 0" id="allInButton" :is-dice-button="false">
    </dice-cup-action-button-component>
    <dice-cup-action-button-component @dice="dice" :disabled="remainingDices < 0 || !active" :is-dice-button="true">
    </dice-cup-action-button-component>
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
</style>
