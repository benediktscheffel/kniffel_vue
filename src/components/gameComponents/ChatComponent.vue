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
<!--      <div @click="closeChat" style="cursor: pointer; position: absolute; top: 5px; right: 10px; z-index: 13; color: lightgrey;">
        <p>X</p>
      </div>-->
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
      document.body.style.overflow = 'auto'
      chatBtn.style.visibility = 'visible'
    },
    hideChatButton () {
      const chatBtn = document.querySelector('.chatButton')
      document.body.style.overflow = 'hidden'
      chatBtn.style.visibility = 'hidden'
    }
    /*
    ,
    closeChat () {
      const chat = document.getElementById('chatMenu')
      chat.style = 'visibility: hidden'
      this.showChatButton()
    }
    */
  }
}
</script>

<style scoped>

.chatContainer {
  width: 350px;
  max-height: 90%;
  justify-self: center;
}

@media screen and (max-width: 600px) {

}

@media screen and (max-width: 450px) {
  .chatContainer{
    width: 343px;
    display: flex;
    justify-self: center;
    max-width: 375px;
  }

  .q-menu {
    justify-content: center !important;
  }
}

@media screen and (max-width: 350px) {
  .chatContainer{
    max-width: 300px;
  }
  .q-menu {
    justify-content: center !important;
  }
}
.chatButton {
  position: fixed;
  bottom: 0;
  right: 0;
}

.q-menu {
  /* right: 17px; */
  /* bottom: 60px; */
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
  /* width: 400px; */
  color: white;

}

</style>
