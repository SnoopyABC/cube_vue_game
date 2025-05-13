<script setup lang="ts">
import { ref } from 'vue'
import ThreeCnavas from './ThreeCanvas.vue'
import RotateButton from './RotateButton.vue'

const animateRotation = () => {
  canvasRef.value?.rotateOnce()
};

const canvasRef = ref<InstanceType<typeof ThreeCnavas>>(null)

</script>


<template>
  <main>

    <ThreeCnavas ref="canvasRef"></ThreeCnavas>
    <RotateButton @rotate="animateRotation" />
  </main>
</template>
