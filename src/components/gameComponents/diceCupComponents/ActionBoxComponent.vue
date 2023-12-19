<script>
import DiceCupActionButtonComponent from 'components/gameComponents/diceCupComponents/DiceCupActionButtonComponent.vue'
import RemainingDiceImageComponent from "components/gameComponents/diceCupComponents/RemainingDiceImageComponent.vue"
export default {
  components: {
    DiceCupActionButtonComponent,
    RemainingDiceImageComponent
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
    <remaining-dice-image-component id="remDice3" :opacity="remainingDices < 2 ? 0.3 : 1"></remaining-dice-image-component>
    <remaining-dice-image-component id="remDice2" :opacity="remainingDices < 1 ? 0.3 : 1"></remaining-dice-image-component>
    <remaining-dice-image-component id="remDice1" :opacity="remainingDices < 0 ? 0.3 : 1"></remaining-dice-image-component>
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
