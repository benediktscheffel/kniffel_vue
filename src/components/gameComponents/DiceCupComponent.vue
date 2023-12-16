<template>
  <q-page class="q-pa-md">
    <q-container class="q-pa-md">
      <q-row align="center" justify="center">
        <q-col>
          <q-card>
            <q-card-section>
              <in-cup-component :incup="incup" :active="active" @putOut="putOut"></in-cup-component>
            </q-card-section>

            <q-card-section>
              <action-box-component :remainingDices="remainingDices" :active="active" @putAllIn="putAllIn"
                                    @dice="dice"></action-box-component>
            </q-card-section>

            <q-card-section>
              <dice-storage-component :stored="stored" :active="active" @putIn="putIn"></dice-storage-component>
            </q-card-section>
          </q-card>
        </q-col>
      </q-row>
    </q-container>
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
    putOut(diceValue) {
      // Your putOut method logic here
    },
    putAllIn() {
      // Your putAllIn method logic here
    },
    dice() {
      // Your dice method logic here
    },
    putIn(diceValue) {
      // Your putIn method logic here
    },
  },
};
</script>

<style scoped>
/* Your component-specific styles here */
</style>
