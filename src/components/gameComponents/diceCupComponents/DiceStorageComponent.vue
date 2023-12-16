<!-- DiceStorage.vue -->
<template>
  <div class="dice-storage" id="diceStorage">
    <div id="diceStorage">
      <div
        v-for="(diceValue, index) in stored"
        :key="index"
        @click="putIn(diceValue)"
        :class="'dice dice_' + diceValue + ' stored'"
        :value="diceValue"
        :style="{ visibility: 'visible', pointerEvents: active ? 'unset' : 'none' }"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    stored: Array,
    active: Boolean,
  },
  methods: {
    putIn(diceValue) {
      // Emit an event or perform logic
    },
  },
};
</script>

<style scoped>
/* Your component-specific styles here */
</style>
