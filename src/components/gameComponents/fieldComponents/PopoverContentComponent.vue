<script>
export default {
  data () {
    return {
      bottomPart: {
        9: '3X',
        10: '4X',
        11: 'home',
        12: 'small_street.png',
        13: 'big_street.png',
        14: '5X',
        15: 'support'
      }
    }
  },
  props: {
    currentPlayer: Number,
    matrix: Array
  }
}
</script>
<template>
  <table class="popover-table">
    <q-tr>
      <template v-for="row in this.matrix.length" :key="row">
        <template v-if="this.matrix[row - 1][this.currentPlayer] === ''">
          <q-td v-if="row < 7">
            <q-img :src="'src/assets/images/' + row + '.png'" />
          </q-td>
        </template>
      </template>
    </q-tr>
    <q-tr>
      <template v-for="row2 in this.matrix.length" :key="row2">
        <template v-if="this.matrix[row2 - 1][this.currentPlayer] === ''">
          <q-td v-if="row2 === 10 || row2 === 11 || row2 === 15">
            <div>{{this.bottomPart[row2 - 1]}}</div>
          </q-td>
          <q-td v-else-if="row2 === 12 || row2 === 16">
            <q-icon :name="this.bottomPart[row2 - 1]" />
          </q-td>
          <td v-else-if="row2 === 13 || row2 === 14">
            <img :src="'src/assets/images/' + this.bottomPart[row2 - 1]"/>
          </td>
        </template>
      </template>
    </q-tr>
  </table>
</template>
<style>
.popover-table td{
  height: 45px;
  border: 1px solid black;
  text-align: center;
  color: black;
  width: 45px;
}

.popover-table span{
  font-size: 30px;
}

.popover-table div{
  font-size: 20px;
  font-weight: bolder;
}

.popover-table i {
  font-size: 25px;
}

.popover-table img {
  height: 100%;
}

</style>
