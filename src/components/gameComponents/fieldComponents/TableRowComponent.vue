<script>
import TableCellComponent from 'components/gameComponents/fieldComponents/TableCellComponent.vue'

export default {
  data() {
    return {
      firstColumn: [
        'src/assets/images/3_mal_1.png', 'src/assets/images/3_mal_2.png', 'src/assets/images/3_mal_3.png',
        'src/assets/images/3_mal_4.png', 'src/assets/images/3_mal_5.png', 'src/assets/images/3_mal_6.png', 'total', 'bonus from 63',
        'total top part', 'three of a kind', 'four of a kind', 'Full-House', 'Small Street', 'Big Street',
        'Kniffel', 'Chance',
        'total bottom part', 'total top part', 'grand total'
      ],
      secondColumn: [
        'only ones count', 'only twos count', 'only threes count', 'only fours count',
        'only fives count', 'only sixes count', 'src/assets/images/right_arrow.png', 'plus 35',
        'src/assets/images/right_arrow.png',
        'all pips count', 'all pips count', '25 points', '30 points', '40 points', '50 points', 'all pips count',
        'src/assets/images/right_arrow.png', 'src/assets/images/right_arrow.png', 'src/assets/images/right_arrow.png'
      ]
    }
  },
  components: {
    TableCellComponent
  },
  props: {
    row: Number,
    active: Boolean,
    matrix: Array,
    currentPlayer: Number,
    numberOfPlayers: Number,
    suggestions: Object
  },
  emits: ['writeTo'],
  methods: {
    writeTo() {
      this.$emit('writeTo', this.row)
    }
  }
}
</script>
<template>
  <template v-if="this.row <= 6">
    <table-cell-component @writeTo="this.writeTo" :has-action-btn="true" :action-btn-row="this.row"
                          :action-btn-active="(!this.active)||(matrix.length > 0&&matrix[row-1][currentPlayer]!=='')"
                          :action-btn-action-text="this.firstColumn[row-1]"
                          :action-btn-img-src="this.firstColumn[row-1]"></table-cell-component>
    <table-cell-component class-attribute="secondColumn" :has-content="true"
                          :cell-content="this.secondColumn[row-1]"></table-cell-component>
  </template>
  <template v-else-if="(row-1) > 8 && (row-1) < 16">
    <table-cell-component @writeTo="this.writeTo" :has-action-btn="true" :action-btn-row="this.row"
                          :action-btn-active="(!this.active)||(matrix.length > 0&&matrix[row-1][currentPlayer]!=='')"
                          :action-btn-action-text="this.firstColumn[row-1]"
                          :action-btn-img-src="this.firstColumn[row-1]"></table-cell-component>
    <table-cell-component class-attribute="secondColumn" :has-content="true"
                          :cell-content="this.secondColumn[row-1]"></table-cell-component>
  </template>
  <template v-else>
    <table-cell-component :has-content="true" :cell-content="this.firstColumn[row-1]"></table-cell-component>
    <template v-if="row === 8">
      <table-cell-component class-attribute="secondColumn" :has-content="true"
                            :cell-content="this.secondColumn[row-1]"></table-cell-component>
    </template>
    <template v-else>
      <table-cell-component class-attribute="secondColumn" :has-icon="true"
                            icon="arrow_right_alt"></table-cell-component>
    </template>
  </template>
  <template v-for="col in this.numberOfPlayers" :key="col">
    <template v-if="(col-1) === this.currentPlayer">
      <template v-if="this.suggestions !== undefined && this.suggestions[row - 1] !== undefined">
        <table-cell-component class-attribute="activeCol" :has-span="true" span-class-attribute="cell"
                              :span-content="this.matrix[this.row-1][col - 1]"
                              :placeholder="this.suggestions[row - 1].toString()"
                              @writeTo="writeTo"></table-cell-component>
      </template>
      <template v-else>
        <table-cell-component class-attribute="activeCol" :has-span="true" span-class-attribute="cell"
                              :span-content="this.matrix[this.row-1][col - 1]"
                              :placeholder="''" :active="true"></table-cell-component>
      </template>
    </template>
    <template v-else>
      <table-cell-component :has-span="true" span-class-attribute="cell"
                            :span-content="this.matrix[this.row-1][col - 1]"
                            :placeholder="''" :active="false"></table-cell-component>
    </template>
  </template>
</template>
<style>

</style>
