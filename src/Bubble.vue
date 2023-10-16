<template>
  <div data-theme="bumblebee" class="min-h-screen bg-base-200">
    <div class="navbar bg-primary text-primary-content">
      <a class="btn btn-ghost normal-case text-xl" href="#/">charts io</a>
    </div>
    <div class="drawer">
      <input id="my-drawer" type="checkbox" class="drawer-toggle" checked />
      <div class="drawer-content">
        <!-- Page content here -->
        <div class="w-full flex justify-center items-center">
          <label
            for="my-drawer"
            class="btn btn-primary m-4 drawer-button px-10 text-center"
            >edit chart</label
          >
        </div>
        <button
          @click="exportData"
          class="btn btn-success py-4 px-8 fixed right-4 bottom-4"
        >
          Export
        </button>
        <div class="w-full flex justify-center">
          <div class="w-11/12">
            <canvas ref="myBubbleChart" class="mb-20"></canvas>
          </div>
        </div>
      </div>
      <div class="drawer-side">
        <label
          for="my-drawer"
          aria-label="close sidebar"
          class="drawer-overlay"
        ></label>

        <ul
          class="menu p-4 w-sm max-w-sm min-w-sm min-h-full bg-base-200 text-base-content z-[1]"
        >
          
          <div v-for="(bubble, index) in bubbleChartData" :key="index">
            <div class="w-full flex flex-row m-0 p-0 py-2">
              <div class="flex items-center join">
                <input
                  v-model.number="bubble.x"
                  type="number"
                  @input="updateBubble"
                  class="w-1/4 input input-bordered join-item"
                  placeholder="X Coordinate"
                />
                <input
                  v-model.number="bubble.y"
                  type="number"
                  @input="updateBubble"
                  class="w-1/4 input input-bordered join-item"
                  placeholder="Y Coordinate"
                />
                <input
                  v-model.number="bubble.r"
                  type="number"
                  @input="updateBubble"
                  class="w-1/4 input input-bordered join-item"
                  placeholder="Radius"
                />
              </div>
              <div class="divider"></div>
              <div class="flex justify-end max-w-sm">
                <button class="btn btn-error" @click="removeBubble(index)">
                  <svg
                    xmlns="http://www.w3.org/2000/svg"
                    fill="none"
                    viewBox="0 0 24 24"
                    stroke-width="1.5"
                    stroke="currentColor"
                    class="w-6 h-6"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0"
                    />
                  </svg>
                </button>
              </div>
            </div>
          </div>
          <div class="w-full flex justify-center">
                <button class="btn w-full btn-primary" @click="addNewBubble">
                  new bubble
                </button>
            </div>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import Chart from "chart.js/auto";
import * as FileSaver from "file-saver";

export default {
  name: "InteractiveBubbleChart",
  data() {
    return {
      bubbleChartData: [
        {
          x: 10,
          y: 20,
          r: 8,
        },
        {
          x: 15,
          y: 10,
          r: 8,
        },

        {
          x: 15,
          y: 10,
          r: 8,
        },

        {
          x: 15,
          y: 10,
          r: 8,
        },
        {
          x: 9,
          y: 6,
          r: 8,
        },

        {
          x: 4,
          y: 1,
          r: 8,
        },

        {
          x: 6,
          y: 10,
          r: 8,
        },
        // Add more bubble data objects as needed
      ],
    };
  },
  mounted() {
    this.renderBubbleChart();
  },
  methods: {
    renderBubbleChart() {
      const ctx = this.$refs.myBubbleChart.getContext("2d");
      this.bubbleChart = new Chart(ctx, {
        type: "bubble",
        data: {
          datasets: [
            {
              label: "Bubble Chart",
              data: this.bubbleChartData,
              backgroundColor: "rgba(255, 99, 132, 0.6)",
            },
          ],
        },

        options: {
          plugins: {
            legend: {
              display: false,
            },
          },
        },
      });
    },

    exportData() {
      //export to png
      const canvas = this.$refs.myBubbleChart;
      const dataURL = canvas.toDataURL("image/png");
      const blob = this.dataURItoBlob(dataURL);
      FileSaver.saveAs(blob, "chart.png");
    },

    dataURItoBlob(dataURI) {
      const byteString = atob(dataURI.split(",")[1]);
      const mimeString = dataURI.split(",")[0].split(":")[1].split(";")[0];
      const ab = new ArrayBuffer(byteString.length);
      const ia = new Uint8Array(ab);
      for (let i = 0; i < byteString.length; i++) {
        ia[i] = byteString.charCodeAt(i);
      }
      return new Blob([ab], { type: mimeString });
    },

    addNewBubble() {
      this.bubbleChartData = [
        ...this.bubbleChartData,
        {
          x: Math.round(Math.random() * 10),
          y: Math.round(Math.random() * 10),
          r: 8,
        },
      ];
      this.updateBubble();
    },

    removeBubble(index) {
      this.bubbleChartData = this.bubbleChartData.filter((_, i) => i !== index);
      this.updateBubble();
    },

    updateBubble() {
      const updatedData = this.bubbleChartData.map((bubble) => {
        return { x: bubble.x, y: bubble.y, r: bubble.r };
      });
      this.bubbleChart.data.datasets[0].data = updatedData;
      this.bubbleChart.update();
    },
  },
};
</script>

