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
  max-width: 600px;
  min-width: 400px;
  margin: 2% 35%;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}
.q-card {
  display: flex;
  justify-content: center;
  align-items: center;
  background: url("src/assets/images/wood.png");
  border-radius: 30px;
  box-shadow: #1a1d20;
  max-width: 600px;
  max-height: 400px;
}

@media screen and (max-width: 600px) {
  .board {
    max-width: 500px;
    min-width: 200px;
    margin: 2% 10%;
  }

  .q-card {
    max-width: 600px;
    min-width: 200px;
  }
}

@media screen and (max-width: 450px) {
  .board {
    max-width: 440px;
    min-width: 200px;
    margin: 2% 10%;
    scale: 95%;
  }

  .q-card {
    max-width: 450px;
    min-width: 200px;
  }
}
@media screen and (max-width: 350px) {
  .board {
    max-width: 340px;
    min-width: 200px;
    margin: 2% 20%;
    scale: 78%;
  }

  .q-card {
    max-width: 350px;
    min-width: 200px;
  }
}

main.q-page.q-pa-md {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: unset !important;
}
</style>
