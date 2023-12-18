<script>
import PopoverContentComponent from 'components/gameComponents/fieldComponents/PopoverContentComponent.vue'
import $ from 'jquery';
export default {
  data () {
    return {
      showing: false
    }
  },
  components: {
    PopoverContentComponent
  },
  props: {
    isFirstCol: Boolean,
    isSecondCol: Boolean,
    currentPlayer: Number,
    matrix: Array,
    playerName: String
  },
  methods: {
    zoomIntoField () {
      const thScrollDown = document.getElementById('scrollDown')
      thScrollDown.onclick = function () {
        document.querySelector('.tableContainer').scrollIntoView()
      }
    },
    restart () {
      $.ajax({
        url: 'http://localhost:9000/restart', type: 'GET',
        success: () => {
          window.location.href = '/'
        }
      })
    }
  }
}
</script>
<template>
  <q-th>
    <template v-if="this.isFirstCol">
      <button type="button" id="scrollDown" class="btn btn-block" @click="zoomIntoField">
        <span class="material-symbols-outlined">expand_content</span>
      </button>
      <q-btn type="button" class="btn btn-block" @click="restart">restart</q-btn>
    </template>
    <template v-else-if="this.isSecondCol">
      <q-btn @mouseover="showing = true" @mouseleave="showing = false" class="btn btn-dark popoverButton">Available Options
        <q-menu v-model="showing" anchor="bottom left" self="top left" @mouseover="showing = true" @mouseleave="showing = false">
          <q-item><popover-content-component :current-player="this.currentPlayer" :matrix="this.matrix"></popover-content-component></q-item>
        </q-menu>
      </q-btn>
    </template>
    <template v-else>
      {{this.playerName}}
    </template>
  </q-th>
</template>
<style>
.q-menu.scroll {
  overflow: hidden;
}
.popoverButton {
  text-transform: unset;
  padding: 6px 20px;
}
</style>
