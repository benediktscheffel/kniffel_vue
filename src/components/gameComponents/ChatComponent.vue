<template>
  <q-page v-if="showChat" class="q-pa-md">

    <q-card>
      <q-card-section>
        <q-btn flat round size="md" icon="close" class="q-ma-md" style="float: right" @click="toggleShowChat"/>
        <h1 class="q-mb-md">Chat-Room</h1>

        <q-form @submit.prevent="sendChatMessage">
          <q-input
            v-model="messageContent"
            label="Your comment"
            placeholder="Here is my message.."
            dense
            type="textarea"
          />
          <q-btn type="submit" label="Send" color="primary" class="q-mt-md"/>
        </q-form>

        <div class="q-mt-md">
          <ul class="list-unstyled" id="list">
            <li v-for="chatMessage in chatMessages" :key="chatMessage.id">
              {{ chatMessage.content }} (posted
              <span class="date">{{ calculateMinutesAgo(chatMessage.created_at) }} minutes ago</span>)
              by {{ chatMessage.author }}
            </li>
          </ul>
          <q-btn flat icon="refresh" class="q-mt-md"/>
        </div>
      </q-card-section>
    </q-card>
  </q-page>

  <q-btn
    fab
    fixed
    bottom-right
    icon="chat"
    class="q-ma-md"
    @click="toggleShowChat"
  />
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
  },
  emits: ['sendChatMessage'],
  methods: {
    toggleShowChat() {
      this.showChat = !this.showChat;
    },
    sendChatMessage() {
      this.$emit('sendChatMessage', this.messageContent)

    },
    calculateMinutesAgo(created_at) {
      return Math.round((new Date() - new Date(created_at)) / 60000)
    },
  },
};
</script>

<style scoped>
/* Your styles here */
</style>
