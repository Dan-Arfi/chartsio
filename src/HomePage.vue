<template>
  <div data-theme="bumblebee" style="position: relative; overflow: hidden">
    <div
      class="fixed inset-0 w-screen bg-base-100 bg-[linear-gradient(to_right,#80808012_1px,transparent_1px),linear-gradient(to_bottom,#80808012_1px,transparent_1px)] bg-[size:24px_24px]"
      style="z-index: 0"
    ></div>
    <div class="navbar bg-primary absolute top-0 text-primary-content">
      <a class="btn btn-ghost normal-case text-xl" href="#/">charts io</a>
    </div>

    <div class="hero min-h-screen bg-base-200">
      <div class="hero-content text-center flex flex-col m-0 p-0 mt-20">
        <div class="max-w-xl">
          <h1 class="text-6xl font-bold">
            create beautiful
            <span class="font-extrabold text-primary"> charts</span> in seconds!
          </h1>
          <p class="py-6">
            a user-friendly web app that lets you effortlessly create stunning
            📊 charts in seconds. Unleash your data's potential with beautiful
            📈 bar and 🍰 pie charts. Simplify data visualization like never
            before!
          </p>
        </div>
        <div
          class="w-screen flex-col flex justify-evenly mx-0 px-0 items-center"
        >
          <div
            class="w-screen flex-col flex justify-evenly mx-0 px-0 items-center md:flex-row"
          >
            <a href="#/line" class="mb-5 mx-0 px-0">
              <div
                class="card card-compact w-96 bg-base-100 shadow-xl border-transparent border-4 hover:border-primary"
              >
                <figure>
                  <img
                    src="@/assets/line.png"
                    alt="Shoes"
                    height="192px"
                    style="width: auto; height: 192px"
                  />
                </figure>
                <div class="card-body">
                  <h2 class="card-title">Line chart</h2>

                  <div class="card-actions justify-center w-full">
                    <button class="btn btn-primary w-full">create</button>
                  </div>
                </div>
              </div>
            </a>
          </div>
          <div
            class="w-screen flex-col flex justify-evenly mx-0 px-0 items-center md:flex-row"
          >
            <a href="#/bar" class="mb-5 mx-0 px-0">
              <div
                class="card card-compact w-96 bg-base-100 shadow-xl border-transparent border-4 hover:border-primary"
              >
                <figure>
                  <img src="@/assets/bar.png" alt="Shoes" />
                </figure>
                <div class="card-body">
                  <h2 class="card-title">Bar chart</h2>

                  <div class="card-actions justify-center w-full">
                    <button class="btn btn-primary w-full">create</button>
                  </div>
                </div>
              </div>
            </a>
            <a href="#/pie" class="mb-5 mx-0 px-0">
              <div
                class="card card-compact w-96 bg-base-100 shadow-xl border-transparent border-4 hover:border-primary"
              >
                <figure>
                  <img
                    src="@/assets/pie1.png"
                    alt="Shoes"
                    height="192px"
                    style="width: auto; height: 192px"
                  />
                </figure>
                <div class="card-body">
                  <h2 class="card-title">Pie chart</h2>

                  <div class="card-actions justify-center w-full">
                    <button class="btn btn-primary w-full">create</button>
                  </div>
                </div>
              </div>
            </a>
          </div>
          <div
            class="w-screen flex-col flex justify-evenly mx-0 px-0 items-center md:flex-row"
          >
            <a href="#/doughnut" class="mb-5 mx-0 px-0">
              <div
                class="card card-compact w-96 bg-base-100 shadow-xl border-transparent border-4 hover:border-primary"
              >
                <figure>
                  <img
                    src="@/assets/doughnut.png"
                    alt="Shoes"
                    height="192px"
                    style="width: auto; height: 192px"
                  />
                </figure>
                <div class="card-body">
                  <h2 class="card-title">Doughnut chart</h2>

                  <div class="card-actions justify-center w-full">
                    <button class="btn btn-primary w-full">create</button>
                  </div>
                </div>
              </div>
            </a>

            <a href="#/bubble" class="mb-5 mx-0 px-0">
              <div
                class="card card-compact w-96 bg-base-100 shadow-xl border-transparent border-4 hover:border-primary"
              >
                <figure>
                  <img
                    src="@/assets/bubble.png"
                    alt="Shoes"
                    height="192px"
                    style="width: auto; height: 192px"
                  />
                </figure>
                <div class="card-body">
                  <h2 class="card-title">Bubble chart</h2>

                  <div class="card-actions justify-center w-full">
                    <button class="btn btn-primary w-full">create</button>
                  </div>
                </div>
              </div>
            </a>
          </div>
        </div>
      </div>
    </div>
    <footer
      class="footer footer-center p-10 bg-primary text-primary-content"
      style="position: relative; z-index: 1"
    >
      <aside>
        <p class="font-bold">
          charts io <br />
          created by
          <a href="https://github.com/Dan-Arfi" class="underline">Dan Arfi</a>
        </p>
        <p>Copyright © 2023 - All right reserved lol</p>
      </aside>
    </footer>
  </div>
</template>

<script>
export default {
  name: "App",
  metaInfo: {
      title: 'My Example App',
      titleTemplate: '%s - Yay!',
      htmlAttrs: {
        lang: 'en',
        amp: true
      }
    }
};
</script>
