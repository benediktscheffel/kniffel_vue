<script>
export default {
  props: {
    incup: Array,
    active: Boolean,
  },
  methods: {
    putOut(diceValue) {
      this.$emit('putOut', diceValue)
    },
  },
};
</script>

<template>
  <div class="cup">
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
#diceInCup {
  padding: 52px 65px;
  width: 290px;
  display: inline-block;
  position: relative;
  left: -32px;
  top: 0px;
  visibility: hidden;
}

.dice.inCup {
  margin: 5px;
  position: absolute;
}

.d1 {
  -ms-transform: rotate(86deg);
  -webkit-transform: rotate(86deg);
  transform: rotate(86deg)
}

.d2 {
  -ms-transform: rotate(62deg);
  -webkit-transform: rotate(62deg);
  transform: rotate(62deg);
  left: 120px
}

.d3 {
  -ms-transform: rotate(196deg);
  -webkit-transform: rotate(196deg);
  transform: rotate(196deg);
  left: 170px
}

.d4 {
  -ms-transform: rotate(345deg);
  -webkit-transform: rotate(345deg);
  transform: rotate(345deg);
  top: 100px
}

.d5 {
  -ms-transform: rotate(190deg);
  -webkit-transform: rotate(190deg);
  transform: rotate(190deg);
  top: 100px;
  left: 120px
}

.dice {
  width: 43px;
  height: 43px;
  float: left;
  margin: auto;
}

.dice:hover {
  cursor: pointer;
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

@keyframes shake {
  10%, 90% {
    transform: translate3d(-4px, -4px, 0)
  }
  20%, 80% {
    transform: translate3d(8px, 8px, 0)
  }
  30%, 50%, 70% {
    transform: translate3d(-16px, -16px, 0)
  }
  40%, 60% {
    transform: translate3d(16px, 16px, 0)
  }
}

.cup {
  width: 227px;
  height: 229px;
}

</style>
