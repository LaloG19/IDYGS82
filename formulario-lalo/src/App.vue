<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <div class="container">
    <RouterView />
  </div>
</template>

<style scoped>
.container {
  width: 100%;
  margin: auto;
  text-align: center;
  display: flex;
}
</style>
