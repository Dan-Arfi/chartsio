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
          <!-- <button class=" btn btn-info" @click="renderChart">randomize</button> -->
          
        </div>
        <button
          @click="exportData"
          class="btn btn-success py-4 px-8 fixed right-4 bottom-4"
        >
          Export
        </button>
        <div class="w-full flex justify-center">
            <div class="p-4 chart-container w-full  max-w-xl">
          <canvas
            ref="myChart"
            class="mb-20"
            
          ></canvas>
        </div>
        </div>
      </div>
      <div class="drawer-side">
        <label
          for="my-drawer"
          aria-label="close sidebar"
          class="drawer-overlay"
        ></label>
        <!-- my-drawer -->

        <ul
          class="menu p-4 w-sm max-w-sm min-w-sm min-h-full bg-base-200 text-base-content z-[1]"
        >
          <div class="bg-dark flex justify-end">
            <button
              type="button"
              aria-controls="my-drawer"
              class="bg-error text-black bg-transparent hover:bg-gray-200 hover:text-gray-900 rounded-lg text-sm w-8 h-8 top-2.5 right-2.5 inline-flex items-center justify-center dark:hover:bg-gray-600 dark:hover:text-white"
              @click="closeDrawer"
            >
              <svg
                class="w-3 h-3"
                aria-hidden="true"
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 14 14"
              >
                <path
                  stroke="currentColor"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="m1 1 6 6m0 0 6 6M7 7l6-6M7 7l-6 6"
                />
              </svg>
              <span class="sr-only">Close menu</span>
            </button>
          </div>
          <li v-for="(data, index) in chartData" :key="index">
            <div class="w-full flex flex-row m-0 p-0 py-2">
              <div class="flex items-center join">
                <!-- // dropdown -->
                <div class="dropdown dropdown-hover join-item">
                  <label
                    tabindex="0"
                    class="btn join-item"
                    :style="{ backgroundColor: data.backgroundColor }"
                    >color</label
                  >
                  <ul
                    tabindex="0"
                    class="dropdown-content z-[1] menu p-2 shadow bg-base-200 rounded-lg"
                    style="
                      display: grid;
                      grid-template-columns: repeat(5, 1fr);
                      gap: 5px;
                    "
                  >
                    <li v-for="color in colors" :key="color">
                      <a
                        @click="updateChartColor(index, color)"
                        :style="{ backgroundColor: color }"
                        class="p-5 hover:scale-125"
                      ></a>
                    </li>
                  </ul>
                </div>
                <!--  -->
                <input
                  v-model="data.label"
                  @input="updateChart"
                  class="w-3/4 input input-bordered join-item"
                  style="margin-right: 0"
                />
              </div>
              <div class="divider"></div>

              <div class="flex justify-end join max-w-sm">
                <input
                  class="w-2/4 input input-bordered join-item"
                  type="number"
                  v-model.number="data.value"
                  @input="updateChart"
                  style="margin-right: 0"
                />
                <button
                  class="btn btn-error join-item"
                  @click="removeColumn(index)"
                  style="margin-left: 0"
                >
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
          </li>
          
            <div class="w-full flex justify-center">
                <button class="btn w-full btn-primary" @click="addNewColumn">
                  new slice
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
  name: "InteractivePieChart",
  data() {
    return {
      chartData: [
        {
          label: "slice 1",
          value: Math.round(Math.random() * 20 + 1),
          backgroundColor: "rgba(255, 99, 132)",
        },
        {
          label: "slice 2",
          value: Math.round(Math.random() * 20 + 1),
          backgroundColor: "rgba(54, 162, 235)",
        },
        {
          label: "slice 3",
          value: Math.round(Math.random() * 20 + 1),
          backgroundColor: "rgba(255, 206, 86)",
        },
        {
          label: "slice 4",
          value: Math.round(Math.random() * 20),
          backgroundColor: "rgba(75, 192, 192)",
        },
        {
          label: "slice 5",
          value: Math.round(Math.random() * 20),
          backgroundColor: "rgba(153, 102, 255)",
        },
      ],
      newColumnName: "slice 6",
      newColumnColor: "rgba(255, 159, 64)",

      colors: [
        "#264653",
        "#2a9d8f",
        "#e9c46a",
        "#f4a261",
        "#e76f51",
        "#e63946",
        "#f1faee",
        "#a8dadc",
        "#457b9d",
        "#1d3557",
        "#335c67",
        "#fff3b0",
        "#e09f3e",
        "#9e2a2b",
        "#540b0e",
        "#283d3b",
        "#197278",
        "#edddd4",
        "#c44536",
        "#772e25",
      ],
    };
  },
  mounted() {
    this.renderChart();
  },
  methods: {
    closeDrawer() {
      const drawer = document.getElementById("my-drawer");
      if (drawer.checked) {
        drawer.checked = false;
      }
    },
    updateChartColor(index, color) {
      this.chartData[index].backgroundColor = color;
      this.updateChart();
    },
    exportData() {
      //export to png
      const canvas = this.$refs.myChart;
      const dataURL = canvas.toDataURL("image/png");
      const blob = this.dataURItoBlob(dataURL);
      FileSaver.saveAs(blob, "chart.png");

      // Export to csv
      let csvContent = "";

      // Adding header
      csvContent += "Label,Value\n";

      // Adding data
      this.chartData.forEach((data) => {
        csvContent += `${data.label},${data.value}\n`;
      });

      // Create a Blob and export the file
      const blob1 = new Blob([csvContent]);
      FileSaver.saveAs(blob1, "chart.csv");
    },

    removeColumn(index) {
      this.chartData.splice(index, 1);
      this.updateChart();
    },
    renderChart() {
      const ctx = this.$refs.myChart.getContext("2d");
      this.chart = new Chart(ctx, {
        type: "pie",
        data: {
          labels: this.chartData.map((data) => data.label),
          datasets: [
            {
              label: "Population",
              data: this.chartData.map((data) => data.value),
              backgroundColor: this.chartData.map(
                (data) => data.backgroundColor
              ),
              borderWidth: 1,
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

    updateChart() {
      this.chart.data.labels = this.chartData.map((data) => data.label);
      this.chart.data.datasets[0].data = this.chartData.map(
        (data) => data.value
      );
      this.chart.data.datasets[0].backgroundColor = this.chartData.map(
        (data) => data.backgroundColor
      );
      this.chart.update();
    },
    addNewColumn() {
      if (this.newColumnName.trim() !== "") {
        this.chartData.push({
          label: this.newColumnName,
          value: Math.round(Math.random() * 20 + 1),
          backgroundColor: this.newColumnColor,
        });
        this.newColumnName = "slice " + (this.chartData.length + 1).toString();
        this.updateChart();
      }
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
  },
};
</script>


