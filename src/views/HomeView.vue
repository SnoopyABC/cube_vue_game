<script setup lang="ts">
import { ref } from 'vue'
import ThreeCnavas from './ThreeCanvas.vue'
import RotateButton from './RotateButton.vue'
import GlobalMusicButton from './GlobalMusicButton.vue'
import musicFile from '@/assets/magic.mp3'

const animateRotation = () => {
  canvasRef.value?.rotateOnce()
  const audio = new Audio(musicFile)
  audio.volume = 0.2
  audio.loop = false
  audio.play()
}

const canvasRef = ref<InstanceType<typeof ThreeCnavas>>(null)
</script>

<template>
  <main>
    <ThreeCnavas ref="canvasRef"></ThreeCnavas>
    <div class="button_wrapper">
      <RotateButton @rotate="animateRotation" />
      <GlobalMusicButton />
    </div>
  </main>
</template>

<style scoped>
.button_wrapper {
  position: absolute;
  top: 20px;
  left: 20px;
  display: flex;
  gap: 10px;
}
</style>
