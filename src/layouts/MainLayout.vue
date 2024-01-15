<template>
  <q-layout view="hHh Lpr lFf">
    <nav-bar-component/>
    <offline-component :isOffline="isOffline"></offline-component>

    <q-page-container>
      <router-view/>
    </q-page-container>
  </q-layout>
</template>

<script>
import NavBarComponent from "components/navBarComponent/NavBarComponent.vue";
import OfflineComponent from "components/offlineComponents/OfflineComponent.vue";

export default {
  components: {
    OfflineComponent,
    NavBarComponent,
  },
  data() {
    return {
      isOffline: !navigator.onLine
    }
  },
  created() {
    window.addEventListener('online', this.updateOnlineStatus)
    window.addEventListener('offline', this.updateOnlineStatus)
  },
  destroyed() {
    window.removeEventListener('online', this.updateOnlineStatus)
    window.removeEventListener('offline', this.updateOnlineStatus)
  },
  methods: {
    updateOnlineStatus() {
      this.isOffline = !navigator.onLine
    }
  }
};
</script>

<style>

</style>
