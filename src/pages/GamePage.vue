<template>
  <q-page class="flex flex-center">
    <game-component></game-component>
  </q-page>
</template>

<script>
import {defineComponent} from 'vue'
import GameComponent from "components/gameComponents/GameComponent.vue";

export default defineComponent({
  name: 'GamePage',
  components: {GameComponent}
})
</script>
