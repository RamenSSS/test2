<script setup>
import { RouterView } from 'vue-router'
import HeaderBar from './components/HeaderBar.vue'
</script>

<template>
  <div id="header">
    <HeaderBar />
  </div>
  <div id="content">
    <RouterView />
  </div>
</template>

<style scoped>
</style>