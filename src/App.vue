<script setup lang="ts">
import { RouterView } from 'vue-router'

import PageNavBar from './components/PageNavBar.vue'
</script>

<template>
  <header>
    <PageNavBar />
  </header>
  <main>
    <RouterView />
  </main>
</template>

<style scoped></style>
