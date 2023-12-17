<template>
  <q-page class="q-pa-md">
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
      $.ajax({
        url: '/in', type: 'GET', data: {
          'in': diceElement
        }, success: function (data) {
          this.incup = data.dicecup.incup
          this.stored = data.dicecup.stored
        },
        error: function () {
          console.error('Failed to get dicecup JSON.');
        }
      })

    },
    putOut(diceElement) {
      this.$emit('putOut', diceElement)
    },
    putAllIn() {
      $.ajax({
        url: '/in/all', type: 'GET',
        success: (data) => {
          this.incup = data.dicecup.incup
          this.stored = data.dicecup.stored
        },
        error: function () {
          console.error('Failed to get dicecup JSON.');
        }
      })
    },
  },
};
</script>

<style scoped>
.gameTable td {
  height: 45px;
  border: 1px solid black;
  text-align: center;
  color: black;
  width: 200px;
}

.gameTable th {
  padding: 15px;
  border: 1px solid black;
  text-align: center !important;
  background-color: #9f4045;
  height: 45px;
}

.gameTable th:last-child {
  border-top-right-radius: 20px;
}

.gameTable th:first-child {
  border-top-left-radius: 20px;
}

.gameTable tr:last-child td:first-child {
  border-bottom-left-radius: 20px;
}

.gameTable tr:last-child td:last-child {
  border-bottom-right-radius: 20px;
}

.table-container table {
  background-color: white;
  border-collapse: separate;
  border-spacing: 0;
  scale: 0.9;
  border-radius: 20px;
}

.gameTable td:hover {
  background-color: #e6e6e6;
}

.gameTable tr.main-heading {
  line-height: 10%;
  border: 1px solid black;
}

.gameTable td:first-child {
  background-color: #9f4045;
  color: white;
  font-size: small;
}

.gameTable td.secondColumn {
  border: 1px solid black;
  background-color: #9f4045;
  color: white;
  font-size: small;
}

button.btnAction {
  height: 100%;
  width: 100%;
  border: none;
}

.btnAction img {
  height: 100%;
}

.table-container {
  display: flex;
  justify-content: center;
  margin: auto;
}

.gameTable td.activeCol {
  background-color: lightgrey;
}

.board {
  display: flex;
  justify-content: center;
  align-items: center;
  background-image: url(src/assets/images/wood.png);
  margin: 2% 35%;
  border-radius: 30px;
}

.diceBoard {
  width: 250px;
  height: 250px;

}

.actionBox {
  margin-top: 7px;
  margin-bottom: 7px;
}

.diceStorage {
  width: 85px;
  height: 210px;
  margin-left: 40px;
  display: flex;
  flex-direction: column;
}

.cup {
  background: url('src/assets/images/cup.png') no-repeat;
  width: 227px;
  height: 229px;
  margin: auto;
}

.diceInCup {
  padding: 52px 65px;
  width: 290px;
  display: inline-block;
  position: relative;
  left: -32px;
  top: 10px;
  visibility: hidden;
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

.storage {
  -ms-transform: rotate(0deg);
  -webkit-transform: rotate(0deg);
  transform: rotate(0deg);
}

.play {
  width: 125px !important;
  color: #fff;
  font-size: 17px
}

.hide {
  display: none;
}

.showCup {
  display: block;
  animation: shake 1s cubic-bezier(0.36, 0.07, 0.19, 0.97) both;
  transform: translate3d(0, 0, 0);
  backface-visibility: hidden;
  perspective: 1000px;
  opacity: 1
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


</style>
