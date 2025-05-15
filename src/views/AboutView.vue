<template>
  <div class="about">
    <CustomThreeCanvas ref="canvasRef" />
    <div class="button_wrapper">
      <Button text="Анимация прокрутки" @onClick="handleRotateAnimation" />
      <Button text="Поверунть" @onClick="handleRotation" />
    </div>
  </div>
</template>

<script lang="ts" setup>
import CustomThreeCanvas from './CustomThreeCanvas.vue'
import Button from './Button.vue'
import { ref } from 'vue'

const canvasRef = ref<InstanceType<typeof CustomThreeCanvas> | null>(null)

const handleRotation = () => {
  canvasRef.value?.rotateOnce()
}

const handleRotateAnimation = () => {
  canvasRef.value?.toggleRotateAnimation()
}

</script>


<style>
.button_wrapper {
  position: absolute;
  top: 20px;
  left: 20px;
  display: flex;
  gap: 10px;
}
</style>
