<template>
  <button class="btn" @click="changeMusic">
    ▶️ {{ isAudioPlaying ? 'Выключить' : 'Включить' }} музон
  </button>
</template>

<script setup lang="ts">
import musicFile from '@/assets/general.mp3'
import { ref } from 'vue'

const isAudioPlaying = ref(false)
const audio = new Audio(musicFile)
audio.volume = 0.1
audio.loop = true

const changeMusic = () => {
  if (isAudioPlaying.value) {
    audio.pause()
  } else {
    audio.play()
  }
  isAudioPlaying.value = !isAudioPlaying.value
}
</script>

<style scoped>
.btn {
  z-index: 10;
  padding: 10px 20px;
  font-size: 14px;
  background-color: #222;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
}
.btn:hover {
  background-color: #444;
}
</style>
