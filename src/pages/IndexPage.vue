<template>
  <q-page class="flex flex-center">
    <lobby-component></lobby-component>
  </q-page>
</template>

<script>
import {defineComponent} from 'vue'
import LobbyComponent from "components/lobbyComponents/LobbyComponent.vue";

export default defineComponent({
  name: 'IndexPage',
  components: {LobbyComponent}
})
</script>
