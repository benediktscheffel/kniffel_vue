<template>
  <q-dialog @before-show="scrollToTop" :model-value="isOffline">
    <q-card>
      <q-card-section class="dialogBodyBox">
        <lobby-loading-animation-component/>
        <div class="dialogBodyText">
          <p>You are currently offline.</p>
          <p>Please check your internet connection.</p>
        </div>
      </q-card-section>
    </q-card>
  </q-dialog>
</template>

<script>
import LobbyLoadingAnimationComponent from "components/lobbyComponents/LobbyLoadingAnimationComponent.vue";

export default {
  components: { LobbyLoadingAnimationComponent },
  props: {
    isOffline: Boolean
  },
  methods: {
    scrollToTop() {
      window.scrollTo(0, 0);
    }
  },
};
</script>

<style scoped>
.q-dialog {
  background: unset;
}

.q-card {
  background: #222;
  overflow: hidden;
}

.dialogBodyBox {
  display: flex;
}

.dialogBodyText {
  text-align: center;
  color: white;
}
</style>
