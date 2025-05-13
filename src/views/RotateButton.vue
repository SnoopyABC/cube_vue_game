<template>
  <button class="btn" @click="$emit('rotate')">🔄 Колдуем понос</button>
</template>

<script setup lang="ts">
defineEmits(['rotate'])
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
