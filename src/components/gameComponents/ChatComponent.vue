<template>
  <q-btn
    fab
    fixed
    bottom-right
    icon="chat"
    class="q-ma-md chatButton"
    @click="refreshChat"
  >
    <q-menu anchor="bottom right" self="bottom right">
      <q-item>

        <div class="q-pa-md row justify-center">

          <div style="width: 100%; max-width: 400px">
            <q-scroll-area>
              <q-chat-message
                v-for="chatMessage in chatMessages"
                :key="chatMessage.id"
                :name="chatMessage.author"
                :text="[chatMessage.content]"
                :sent="this.playerName === chatMessage.author"
                :stamp="calculateMinutesAgo(chatMessage.created_at) + ' minutes ago'"
              />
            </q-scroll-area>

          </div>
        </div>

        <q-form @submit.prevent="sendChatMessage">
          <q-input
            rounded outlined
            v-model="messageContent"
            label="Your comment"
            placeholder="Here is my message.."
            type="textarea"

          />
          <q-btn
            :disable="messageContent.length === 0"
            type="submit" label="Send"
            color="primary" class="q-mt-md"
            @click="sendChatMessage"/>
        </q-form>
      </q-item>
    </q-menu>
  </q-btn>
</template>

<script>
export default {
  data() {
    return {
      showChat: false,
      messageContent: '',
    };
  },
  props: {
    chatMessages: Array,
    playerName: String
  },
  emits: ['sendChatMessage', 'refreshChat'],
  methods: {
    sendChatMessage() {
      this.$emit('sendChatMessage', this.messageContent)
      this.messageContent = '';

    },
    calculateMinutesAgo(created_at) {
      return Math.round((new Date() - new Date(created_at)) / 60000)
    },
    refreshChat() {
      this.$emit('refreshChat');
    }
  },
};
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
  max-height: 60%;
}

.q-field__native {
  color: lightgray;
}

.q-item {
  background: #222;
}
</style>
