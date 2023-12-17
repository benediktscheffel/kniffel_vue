<!-- DiceStorage.vue -->
<template>
  <div class="dice-storage" id="diceStorage">
    <div
      v-for="(diceValue, index) in stored"
      :key="index"
      @click="putIn(diceValue)"
      :class="'dice dice_' + diceValue + ' stored'"
      :value="diceValue"
      :style="{ visibility: 'visible', pointerEvents: active ? 'unset' : 'none' }"
    ></div>
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
      this.$emit('putIn', diceValue)
    },
  },
};
</script>

<style scoped>
.dice-storage {
  background: unset;
  -ms-transform: rotate(0deg);
  -webkit-transform: rotate(0deg);
  transform: rotate(0deg);
}

#diceStorage {
  width: 85px;
  height: 210px;
  margin-left: 40px;
  display: flex;
  flex-direction: column;
}


.dice {
  width: 43px;
  height: 43px;
  float: left;
  margin: auto;
}

.dice_1 {
  background: url('src/assets/images/1.png') no-repeat;
  background-size: 100%;
}

.dice_2 {
  background: url('src/assets/images/2.png') no-repeat;
  background-size: 100%;
}

.dice_3 {
  background: url('src/assets/images/3.png') no-repeat;
  background-size: 100%;
}

.dice_4 {
  background: url('src/assets/images/4.png') no-repeat;
  background-size: 100%;
}

.dice_5 {
  background: url('src/assets/images/5.png') no-repeat;
  background-size: 100%;
}

.dice_6 {
  background: url('src/assets/images/6.png') no-repeat;
  background-size: 100%;
}
</style>
