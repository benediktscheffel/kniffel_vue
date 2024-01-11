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
.cup {
  width: 227px;
  height: 229px;
  //scale: 75%;
}
@media screen and (max-width: 600px) {
  .cup {
    width: 165px;
    height: 166px;
  }
  .cup.showCup {
    background-size: 165px !important;
    background-repeat: no-repeat !important;
  }
  #diceInCup {
    left: 0;
  }
}


@media screen and (max-width: 450px) {
  .cup {
    margin-right: 10px;
    width: 165px;
    height: 166px;
  }
  .cup.showCup {
    background-size: 165px !important;
    background-repeat: no-repeat !important;
  }
  #diceInCup {
    left: 0;
  }
}

@media screen and (max-width: 350px) {
  .cup {
    width: 175px;
    height: 100px;
  }
  .cup.showCup {
    background-size: 165px !important;
    background-repeat: no-repeat !important;
  }

  #diceInCup {
    left: 0;
  }
}


#diceInCup {
  padding: 52px 65px;
  width: 290px;
  display: inline-block;
  position: relative;
  left: -32px;
  top: 0px;
  visibility: hidden;
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

.cup {
  width: 190px;
  height: 229px;
}

</style>
