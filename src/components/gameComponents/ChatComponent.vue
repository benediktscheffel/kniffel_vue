<template>
  <q-btn
    fab
    fixed
    bottom-right
    icon="chat"
    class="q-ma-md chatButton"
    @click="refreshChat"
  >
    <q-menu transition-show="rotate"
            transition-hide="rotate"
            id="chatMenu"
            @before-show="hideChatButton"
            @before-hide="showChatButton"
            anchor="bottom right"
            self="bottom right">
      <q-item class="chatContainer">
        <div class="q-pa-md row justify-center" :style="{ overflow: 'unset', height: '100%' }">

          <div style="width: 100%; max-width: 400px">
            <chat-message-component v-for="chatMessage in chatMessages"
                                    :key="chatMessage.id"
                                    :playerName="this.playerName"
                                    :chatMessage="chatMessage">
            </chat-message-component>
          </div>
        </div>
        <chat-form-component @sendChatMessage="sendChatMessage"></chat-form-component>
      </q-item>
    </q-menu>
  </q-btn>
</template>

<script>
import ChatMessageComponent from 'components/gameComponents/chatComponents/ChatMessageComponent.vue'
import ChatFormComponent from 'components/gameComponents/chatComponents/ChatFormComponent.vue'

export default {
  components: {
    ChatMessageComponent,
    ChatFormComponent
  },
  data () {
    return {
      showChat: false
    }
  },
  props: {
    chatMessages: Array,
    playerName: String
  },
  emits: [
    'refreshChat',
    'sendChatMessage'
  ],
  methods: {
    sendChatMessage (messageContent) {
      this.$emit('sendChatMessage', messageContent)
    },
    refreshChat () {
      this.$emit('refreshChat')
    },
    showChatButton () {
      const chatBtn = document.querySelector('.chatButton')
      chatBtn.style.visibility = 'visible'
    },
    hideChatButton () {
      const chatBtn = document.querySelector('.chatButton')
      chatBtn.style.visibility = 'hidden'
    }
  }
}
</script>

<style scoped>
.chatButton {
  position: fixed;
  bottom: 0;
  right: 0;
}

.q-menu {
  right: 17px;
  bottom: 60px;
  left: unset;
  max-width: 10px;
  justify-content: right;
  display: flex;
  flex-direction: column;
  max-height: 60%;
}

.q-btn {
  color: #ffffff;
  background: #55553e;
}

.q-item {
  background: #222;
  display: flex;
  flex-direction: column;
  width: 400px;
  color: white;

}

</style>
