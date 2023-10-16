<script setup>
import { ref } from 'vue'

let message = ref('')

function reset() {
  message.value = ''
}
</script>

<template>
  <div class="input">
    <textarea v-model="message" class="textarea" placeholder="Type your message here..."></textarea>
    <button class="button" @click="$emit('submit', message), reset()">Send</button>
  </div>
</template>

<style scoped>
.input {
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-top: 6px;
}
.textarea {
  flex-grow: 1;
  resize: none;
  max-height: 3em;
}

.button {
  margin-left: 12px;
  width: 60px;
}
</style>
