<!-- DieComponent.vue -->
<template>
  <div
    :class="'dice dice_' + this.diceValue + (this.stored ? ' stored' : ' inCup d' + (this.index + 1))"
    @click="dieClick(this.diceValue)"
    :value="this.diceValue"
    :style="{ visibility: 'visible', cursor: this.active ? 'pointer' : 'not-allowed', pointerEvents: this.active ? 'unset' : 'none' }"
  ></div>
</template>

<script>
export default {
  props: {
    diceValue: Number,
    index: Number,
    stored: Boolean,
    active: Boolean
  },
  methods: {
    dieClick (diceValue) {
      if (this.stored) {
        this.$emit('putIn', diceValue)
      } else {
        this.$emit('putOut', diceValue)
      }
    }
  }
}
</script>

<style scoped>
@media screen and (max-width: 450px) {
  .dice {
    width: 35px;
    height: 35px;
  }
}
@media screen and (max-width: 450px) {
  .d2 {
    left: 110px;
  }
  .d3 {
    left: 157px;
  }
  .d5 {
    left: 110px
  }
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
</style>
