<script setup>
import { ref, computed } from "vue";
import HomePage from "./HomePage.vue";
import Bars from "./Bars.vue";
import NotFound from "./NotFound.vue";
import Pie from "./Pie.vue";
import Doughnut from "./Doughnut.vue";
import Bubble from "./Bubble.vue";
import Line from "./Line.vue";

const routes = {
  "/": HomePage,
  "/bars": Bars,
  "/pie": Pie,
  "/doughnut": Doughnut,
  "/bubble": Bubble,
  "/line": Line,
};

usehe;

const currentPath = ref(window.location.hash);

window.addEventListener("hashchange", () => {
  currentPath.value = window.location.hash;
});

const currentView = computed(() => {
  return routes[currentPath.value.slice(1) || "/"] || NotFound;
});
</script>

<template>
  <!-- <a href="#/">Home</a> |
  <a href="#/bars">Broken Link</a> -->
  <div data-theme="bumblebee"></div>
  <component :is="currentView" />
</template>

<style>
.btn:hover {
  scale: 105%;
  transition: all 0.2s ease;
}
</style>
