<script setup>
import { ref, nextTick } from 'vue'
import ChatBubble from './ChatBubble.vue'
import ChatInput from './ChatInput.vue'

import { currentUser, conversation } from '../api/mockapi'

const currentUserObj = JSON.parse(currentUser)
const conversationObj = JSON.parse(conversation)
const renderComponent = ref(true)

async function sendReply(message) {
  if (!message) return

  renderComponent.value = false

  const messageObj = {
    id: conversationObj.length + 1,
    from: currentUserObj,
    message: message,
    date: new Date().toISOString()
  }
  conversationObj.push(messageObj)

  // not sure why this isn't re-rendering without v-if hack. haven't used vue in a while
  await nextTick()
  renderComponent.value = true

  await nextTick()
  bottom.value?.scrollIntoView({ behavior: 'smooth' })
}

const bottom = ref(null)
</script>

<template>
  <div class="wrapper">
    <div class="window" v-if="renderComponent">
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
