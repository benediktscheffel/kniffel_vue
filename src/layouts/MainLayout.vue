<template>
  <q-layout view="hHh Lpr lFf">
    <!-- Navigation Bar Component -->
    <nav-bar-component/>

    <q-page-container>
      <!-- Content of the page will be rendered here -->
      <router-view/>
    </q-page-container>
  </q-layout>
</template>

<script>
import NavBarComponent from "components/navBarComponent/NavBarComponent.vue";

export default {
  components: {
    NavBarComponent,
  },
};
</script>

<style>

</style>
