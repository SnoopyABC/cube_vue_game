<template>
  <button class="btn" @click="$emit('rotate')">
    🔄 Вращение и цвет
  </button>
</template>

<script setup lang="ts">
defineEmits(['rotate'])
</script>

<style scoped>
.btn {
  position: absolute;
  top: 20px;
  left: 20px;
  z-index: 10;
  padding: 10px 20px;
  font-size: 16px;
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
