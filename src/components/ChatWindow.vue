<script setup>
import { ref, nextTick, reactive } from 'vue'
import ChatBubble from './ChatBubble.vue'
import ChatInput from './ChatInput.vue'

import { currentUser, conversation } from '../api/mockapi'

const currentUserObj = JSON.parse(currentUser)
const conversationObj = reactive(JSON.parse(conversation))

async function sendReply(message) {
  if (!message) return

  const messageObj = {
    id: conversationObj.length + 1,
    from: currentUserObj,
    message: message,
    date: new Date().toISOString()
  }
  conversationObj.push(messageObj)

  await nextTick()

  bottom.value?.scrollIntoView({ behavior: 'smooth' })
}

const bottom = ref(null)
</script>

<template>
  <div class="wrapper">
    <div class="window">
      <ChatBubble
        v-for="{ id, message, from } in conversationObj"
        :key="id"
        :message="message"
        :thumbnail="currentUserObj.thumbnail"
        :inverted="from.id == currentUserObj.id"
      >
      </ChatBubble>
      <div ref="bottom" />
    </div>
    <ChatInput v-model="message" @submit="sendReply" />
  </div>
</template>

<style scoped>
.wrapper {
  display: flex;
  flex-direction: column;
}

.window {
  width: 500px;
  height: 400px;
  border: 2px black solid;
  overflow-y: scroll;
  padding: 12px;
}
</style>
