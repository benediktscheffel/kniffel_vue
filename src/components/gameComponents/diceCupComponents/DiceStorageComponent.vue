<!-- DiceStorage.vue -->
<template>
  <div class="dice-storage" id="diceStorage">
    <die-component @putIn="putIn(diceValue)"
      v-for="(diceValue, index) in stored"
      :key="index"
      :diceValue="diceValue"
      :index="index"
      :stored="true"
      :active="this.active"
    ></die-component>
  </div>
</template>

<script>
import DieComponent from 'components/gameComponents/diceCupComponents/DieComponent.vue'
export default {
  components: {
    DieComponent
  },
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
  width: 75px;
  height: 210px;
  display: flex;
  flex-direction: column;
}
</style>
