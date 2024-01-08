<template>
  <q-chat-message
    :name="this.chatMessage.author"
    :text="[this.chatMessage.content]"
    :sent="this.playerName === this.chatMessage.author"
    :stamp="calculateMinutesAgo(this.chatMessage.created_at) + ' minutes ago'"
  />
</template>

<script>
export default {
  props: {
    chatMessage: Object,
    playerName: String
  },
  methods: {
    calculateMinutesAgo (createdAt) {
      return Math.round((new Date() - new Date(createdAt)) / 60000)
    }
  }
}
</script>

<style scoped>
.q-chat-message {
  align-items: flex-end;
}
</style>
