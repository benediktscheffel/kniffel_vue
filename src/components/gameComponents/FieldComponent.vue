<script>
import TableRowComponent from 'components/gameComponents/fieldComponents/TableRowComponent.vue'
import HeaderTableCellComponent from 'components/gameComponents/fieldComponents/HeaderTableCellComponent.vue'

export default {
  components: {
    TableRowComponent,
    HeaderTableCellComponent
  },
  /* default values
  data () {
    return {
      currentPlayer: 0,
      matrix: [['', ''], ['', ''], ['', ''], ['', ''], ['', ''], ['', '6'], ['0', '6'], ['0', '0'], ['0', '6'], ['', ''], ['', ''], ['', ''], ['30', ''], ['', ''], ['', ''], ['', ''], ['30', '0'], ['0', '6'], ['30', '6']],
      players: [{ id: 0, name: 'a' }, { id: 1, name: 'b' }],
      numberOfPlayer: 2,
      active: true
    }
  }, */
  props: {
    currentPlayer: Number,
    matrix: Array,
    players: Array,
    numberOfPlayers: Number,
    active: Boolean
  },
  methods: {
    writeTo (row) {
      this.$emit('writeTo', (row - 1))
    }
  }
}
</script>

<template>
 <div class="game">
   <div class="tableContainer">
     <table class="gameTable" id="gameTable">
       <thead>
        <q-tr class="main-heading">
          <header-table-cell-component :is-first-col="true"></header-table-cell-component>
          <header-table-cell-component :is-second-col="true" :current-player="this.currentPlayer"
                                       :matrix="this.matrix"></header-table-cell-component>
          <template v-for="col in this.numberOfPlayer" :key="col">
            <header-table-cell-component :player-name="this.players[col-1].name"></header-table-cell-component>
          </template>
        </q-tr>
       </thead>
       <q-tr v-for="row in 19" :key="row">
         <table-row-component @write-to="this.writeTo" :row="row" :active="this.active" :matrix="this.matrix"
                              :current-player="this.currentPlayer" :number-of-players="this.numberOfPlayer">
         </table-row-component>
       </q-tr>
     </table>
   </div>
 </div>
</template>

<style>
.game {
  display: flex;
  flex-direction: column;
  align-items: center;
}

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

.tableContainer table {
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

.tableContainer {
  display: flex;
  justify-content: center;
  margin: auto;
}

.gameTable td.activeCol {
  background-color: lightgrey;
}
</style>
