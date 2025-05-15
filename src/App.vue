<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <div class="nav">
    <RouterLink class="link" to="/">Home</RouterLink>
    <RouterLink class="link" to="/about">Cat 3d Model</RouterLink>
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
a.link,
a.link:active,
a.link:visited,
a.link:focus {
  color: #fff;
  text-decoration: none;
}
a.link:hover{
  text-decoration: underline;
}
</style>
