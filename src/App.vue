<script setup>
import { ref, computed } from "vue";
import HomePage from "./HomePage.vue";
import Bars from "./Bars.vue";
import NotFound from "./NotFound.vue";
import Pie from "./Pie.vue";
import Doughnut from "./Doughnut.vue";
import Bubble from "./Bubble.vue";
import Line from "./Line.vue";
import { useHead } from "@vueuse/head";


const routes = {
  "/": HomePage,
  "/bar": Bars,
  "/pie": Pie,
  "/doughnut": Doughnut,
  "/bubble": Bubble,
  "/line": Line,
};



useHead({
  title: "charts io - beautiful charts in seconds",
  meta: [
    {
      name: "description",
      content: "A user-friendly web app that lets you effortlessly create stunning charts in seconds. Unleash your data's potential with beautiful bar line bubble and pie charts. Simplify data visualization like never before!"
    }
  ]
})


const currentPath = ref(window.location.hash);

window.addEventListener("hashchange", () => {
  currentPath.value = window.location.hash;
});

const currentView = computed(() => {
  return routes[currentPath.value.slice(1) || "/"] || NotFound;
});



</script>

<template>
  <div data-theme="bumblebee"></div>
  <component :is="currentView" />
</template>

<style>
.btn:hover {
  scale: 105%;
  transition: all 0.2s ease;
}
</style>
