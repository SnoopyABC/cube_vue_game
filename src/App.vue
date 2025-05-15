<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <div class="nav">
    <RouterLink to="/">Home</RouterLink>
    <RouterLink to="/about">About</RouterLink>
  </div>
  <RouterView />
</template>

<style scoped>
.nav {
  position: absolute;
  bottom: 0;
  left: 20px;
  display: flex;
  gap: 10px;
}
</style>
