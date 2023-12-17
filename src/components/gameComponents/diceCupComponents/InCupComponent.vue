<script>
export default {
  props: {
    incup: Array,
    active: Boolean,
  },
  methods: {
    putOut(diceValue) {
      // Emit an event or perform logic
      this.$emit('putOut', diceValue)
    },
  },
};
</script>

<template>
  <div class="cup" style="background: none">
    <div class="dice-in-cup" id="diceInCup">
      <div
        v-for="(diceValue, index) in incup"
        :key="index"
        :class="'dice d' + (index + 1) + ' dice_' + diceValue + ' inCup'"
        :value="diceValue"
        :style="{ pointerEvents: active ? 'unset' : 'none', visibility: 'visible' }"
        @click="putOut(diceValue)"
      ></div>
    </div>
  </div>
</template>

<style scoped>
/* Your component-specific styles here */
</style>
