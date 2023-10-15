<script setup>
import { ref, computed } from 'vue'
import HomePage from './HomePage.vue'
import Bars from './Bars.vue'
import NotFound from './NotFound.vue'

const routes = {
  '/': HomePage,
  '/bars': Bars
}

const currentPath = ref(window.location.hash)

window.addEventListener('hashchange', () => {
  currentPath.value = window.location.hash
})

const currentView = computed(() => {
  return routes[currentPath.value.slice(1) || '/'] || NotFound
})
</script>

<template>
  <!-- <a href="#/">Home</a> |
  <a href="#/bars">Broken Link</a> -->
  
  <component :is="currentView" />
  
</template>