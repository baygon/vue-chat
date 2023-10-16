<script setup>
defineProps({
  inverted: {
    type: Boolean
  },
  message: {
    type: String,
    required: true
  },
  thumbnail: {
    type: String,
    required: true
  }
})
</script>

<template>
  <div class="bubble" :class="{ inverted: inverted }">
    <div class="thumbnail">
      <img :src="thumbnail" />
    </div>
    <div class="message">
      {{ message }}
    </div>
  </div>
</template>

<style scoped>
.bubble {
  display: flex;
  align-items: flex-end;
}

.bubble.inverted {
  flex-direction: row-reverse;
}

.message {
  margin: 12px;
  border-radius: 8px;
  padding: 8px;
  background-color: rgb(194, 194, 194);
  max-width: 60%;
}

.inverted .message {
  background-color: rgb(126, 171, 255);
}

.thumbnail {
  height: 48px;
  width: 48px;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
