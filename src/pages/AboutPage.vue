<template>
  <q-page class="flex flex-center">
    <about-component></about-component>
  </q-page>
</template>

<script>
import {defineComponent} from 'vue'
import AboutComponent from "components/aboutComponents/AboutComponent.vue";

export default defineComponent({
  name: 'IndexPage',
  components: {AboutComponent}
})
</script>
