<template>
  <div class="hero min-h-screen bg-base-200" data-theme="dark">
    <div
      class="absolute inset-0 h-full w-full bg-base-100 bg-[linear-gradient(to_right,#80808012_1px,transparent_1px),linear-gradient(to_bottom,#80808012_1px,transparent_1px)] bg-[size:24px_24px]"
    ></div>
    <div class="hero-content text-center flex flex-col m-0 p-0">
      <div class="max-w-md">
        <h1 class="text-5xl font-bold">create charts in second!</h1>
        <p class="py-6">
          Provident cupiditate voluptatem et in. Quaerat fugiat ut assumenda
          excepturi exercitationem quasi. In deleniti eaque aut repudiandae et a
          id nisi.
        </p>
      </div>
      <div class="w-screen flex-row flex justify-evenly mx-0">
        <a href="#/bars">
            <div
          class="w-56 h-56 bg-neutral hover:bg-base-100 cursor-pointer transition-all rounded-box text-center flex justify-center items-center text-5xl"
        >
          BARS
        </div>
        </a>
        <div
          class="w-56 h-56 bg-neutral rounded-box text-center hover:bg-base-100 cursor-pointer transition-all flex justify-center items-center text-5xl"
        >
          PIE
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
};
</script>

<style>
/* Add your custom styles here */
</style>
