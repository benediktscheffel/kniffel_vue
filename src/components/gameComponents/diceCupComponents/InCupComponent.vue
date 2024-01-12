<script>
import DieComponent from 'components/gameComponents/diceCupComponents/DieComponent.vue'

export default {
  components: {
    DieComponent
  },
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
      <die-component @putOut="putOut(diceValue)"
                     v-for="(diceValue, index) in incup"
                     :key="index"
                     :diceValue="diceValue"
                     :index="index"
                     :stored="false"
                     :active="this.active"
      ></die-component>
    </div>
  </div>
</template>

<style scoped>
#diceInCup {
  padding: 52px 65px;
  width: 290px;
  display: inline-block;
  position: relative;
  left: -45px;
  top: 0px;
  visibility: hidden;
}

.cup {
  width: 190px;
  height: 190px;
  background-size: 190px;
}
@media screen and (max-width: 600px) {
  .cup {
    width: 165px;
    height: 165px;
  }
  .cup.showCup {
    background-size: 165px;
    background-repeat: no-repeat;
  }
  #diceInCup {
    left: -55px;
    top: -15px;
  }
}

@media screen and (max-width: 350px) {
  .cup.showCup {
    height: 140px;
    width: 140px;
    background-size: 140px;
    background-repeat: no-repeat !important;
  }

  #diceInCup {
    left: -65px;
    top: -25px;
  }
}

@keyframes shake {
  10%, 90% {
    transform: translate3d(-4px, -4px, 0);
  }
  20%, 80% {
    transform: translate3d(8px, 8px, 0);
  }
  30%, 50%, 70% {
    transform: translate3d(-16px, -16px, 0);
  }
  40%, 60% {
    transform: translate3d(16px, 16px, 0);
  }
}

</style>
