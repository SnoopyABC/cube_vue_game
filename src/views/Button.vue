<template>
  <div @click="$emit('onClick')" class="btn">
    <div>{{ text }}</div>
  </div>
</template>

<script lang="ts" setup>
interface Props {
  text: string
}

const { text } = defineProps<Props>()
</script>

<style scoped>
.btn {
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
