<template>
  <q-dialog :model-value="dialogVisible" persistent @update:model-value="updateConfirmationDialog">
    <q-card>
      <q-card-section class="dialogBodyBox">
          <lobby-loading-animation-component></lobby-loading-animation-component>
          <div class="dialogBodyText">
            <p>
              <span>{{ playersReady }}</span>/<span>{{ playersCount }}</span>
              Players ready
            </p>
            <p>
              <span>Seconds until Start: </span><span>{{ countdown }}</span>
            </p>
          </div>
      </q-card-section>

      <q-card-actions align="center">
        <q-btn
          flat
          color="dark"
          id="ready"
          @click="readyFunction">Ready</q-btn>
        <q-btn flat color="dark" id="leaveLobby" @click="openLeaveDialog">
          Leave
          <span class="material-symbols-outlined">
          <q-icon>exit_to_app</q-icon>
          </span>
        </q-btn>
      </q-card-actions>
    </q-card>
  </q-dialog>
</template>

<script>
import LobbyLoadingAnimationComponent from "components/lobbyComponents/LobbyLoadingAnimationComponent.vue";

export default {
  components: {LobbyLoadingAnimationComponent},
  props: {
    dialogVisible: Boolean,
    playersReady: Number,
    playersCount: Number,
    countdown: String,
    ready: Boolean,
  },
  methods: {
    readyFunction() {
      const readyBtn = document.getElementById('ready')
      readyBtn.style.backgroundColor = 'green'
      readyBtn.style.borderColor = 'green'
      readyBtn.style.display = 'flex'
      readyBtn.style.justifyContent = 'center'
      readyBtn.disabled = true
      const checkSpan = document.createElement('span')
      checkSpan.classList.add('material-symbols-outlined')
      checkSpan.innerText = 'check'
      readyBtn.replaceChildren(checkSpan)
      this.$emit('readyFunction')
    },
    openLeaveDialog() {
      this.$emit('openLeaveDialog');
    },
    updateConfirmationDialog() {
      this.$emit('updateConfirmationDialog');
    }
  },
};
</script>

<style scoped>

.q-card {
  background: #222;
  overflow: hidden;
}

.q-btn {
  background: darkgrey;
}

.dialogBodyBox {
  display: flex;
}

.dialogBodyText {
  text-align: center;
  color: white;
}

#ready {
  width: 100px;
  height: 20px;
}

#leaveLobby {
  width: 100px;
  height: 20px;
}
</style>
