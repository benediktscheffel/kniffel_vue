<template>
  <q-page class="q-pa-md">

    <q-card>
      <div class="board">
        <q-card-section>
          <in-cup-component
            :incup="incup"
            :active="active"
            @putOut="putOut"
          ></in-cup-component>
        </q-card-section>

        <q-card-section>
          <action-box-component
            :remainingDices="remainingDices"
            :active="active"
            @putAllIn="putAllIn"
            @dice="dice"></action-box-component>
        </q-card-section>

        <q-card-section>
          <dice-storage-component
            :stored="stored"
            :active="active"
            @putIn="putIn"
          ></dice-storage-component>
        </q-card-section>
      </div>

    </q-card>
  </q-page>
</template>

<script>
import InCupComponent from "components/gameComponents/diceCupComponents/InCupComponent.vue";
import ActionBoxComponent from "components/gameComponents/diceCupComponents/ActionBoxComponent.vue";
import DiceStorageComponent from "components/gameComponents/diceCupComponents/DiceStorageComponent.vue";

export default {
  components: {
    InCupComponent,
    ActionBoxComponent,
    DiceStorageComponent,
  },
  props: {
    incup: Array,
    remainingDices: Number,
    stored: Array,
    active: Boolean,
  },
  methods: {
    dice() {
      this.$emit('dice')
    },
    putIn(diceElement) {
      this.$emit('putIn', diceElement)
    },
    putOut(diceElement) {
      this.$emit('putOut', diceElement)
    },
    putAllIn() {
      this.$emit('putAllIn')
    },
  },
};
</script>

<style scoped>
.board {
  display: flex;
  justify-content: center;
  align-items: center;
  background-repeat: repeat;
  margin: 2% 35%;
  border-radius: 30px;
}

.diceBoard {
  width: 250px;
  height: 250px;

}

q-card {
  background: url("src/assets/images/wood.png");


}
</style>
