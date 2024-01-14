<template>
  <q-form @submit.prevent="sendChatMessage">
    <q-input
      @focus="scrollDown"
      rounded outlined
      v-model="messageContent"
      color="white"
      :label-color="'white'"
      :input-style="{color: 'white'}"
      label="Your comment"
      placeholder="Here is my message.."
      type="textarea"
    />
    <q-btn
      id="sendBtn"
      :disable="messageContent.length === 0"
      type="submit" label="Send"
      class="q-mt-md"
      @click="sendChatMessage"/>
  </q-form>
</template>

<script>
export default {
  data () {
    return {
      messageContent: ''
    }
  },
  methods: {
    sendChatMessage () {
      this.$emit('sendChatMessage', this.messageContent)
      this.messageContent = ''
    },
    scrollDown () {
      const sendBtn = document.getElementById('sendBtn')
      sendBtn.scrollIntoView()
    }
  },
  emits: ['sendChatMessage']
}
</script>

<style scoped>
form.q-form {
  display: flex;
  flex-direction: column;
  height: 13%;
  color: white;
}

textarea {
  color: white !important;
}

.q-btn {
  color: #ffffff;
  background: #55553e;
}
</style>
