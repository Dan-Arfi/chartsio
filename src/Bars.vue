<template>
  <div data-theme="dark">
    <div class="navbar bg-primary text-primary-content">
      <a class="btn btn-ghost normal-case text-xl" href="#/">charts io</a>
    </div>
    <button
      @click="exportData"
      class="btn btn-primary py-2 px-4 fixed right-4 bottom-4"
    >
      Export
    </button>
    <div class="p-4">
      <table
        class="w-full md:max-w-3xl mx-auto mb-5 rounded-lg border border-separate border-neutral"
      >
        <thead>
          <tr>
            <th class="px-4 py-2">label</th>
            <th class="px-4 py-2">value</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(data, index) in chartData" :key="index">
            <td class="px-4 py-2">
              <div class="flex items-center join">
                <div class="dropdown dropdown-hover join-item">
                  <label
                    tabindex="0"
                    class="btn join-item"
                    :style="{ backgroundColor: data.backgroundColor }"
                    >color</label
                  >
                  <ul
                    tabindex="0"
                    class="dropdown-content z-[1] menu p-2 shadow backdrop-blur-sm bg-white/30 rounded-lg"
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
                <input
                  v-model="data.label"
                  @input="updateChart"
                  class="w-full input input-bordered join-item"
                />
              </div>
            </td>
            <td class="px-4 py-2 flex justify-evenly join">
              <input
                class="w-3/4 input input-bordered join-item"
                type="number"
                v-model.number="data.value"
                @input="updateChart"
              />
              <button class="btn w-1/4 join-item" @click="removeColumn(index)">
                -
              </button>
            </td>
          </tr>
          <tr>
            <td class="px-4 py-2" colspan="2">
              <div class="flex justify-center">
                <button class="btn btn-primary" @click="addNewColumn">
                  new column
                </button>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
      <canvas ref="myChart" class="mt-5" style="max-width: 100%"></canvas>
    </div>
  </div>
</template>

<script>
import Chart from "chart.js/auto";
import * as FileSaver from "file-saver";

export default {
  name: "InteractiveChart",
  data() {
    return {
      chartData: [
        {
          label: "col 1",
          value: Math.round(Math.random() * 20 + 1),
          backgroundColor: "",
        },
        {
          label: "col 2",
          value: Math.round(Math.random() * 20 + 1),
          backgroundColor: "",
        },
        {
          label: "col 3",
          value: Math.round(Math.random() * 20 + 1),
          backgroundColor: "",
        },
        {
          label: "col 4",
          value: Math.round(Math.random() * 20),
          backgroundColor: "",
        },
        {
          label: "col 5",
          value: Math.round(Math.random() * 20),
          backgroundColor: "",
        },
      ],
      newColumnName: "new col",
      newColumnColor: "#ffffff",
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

      startingColors: [
        ["#264653", "#2a9d8f", "#e9c46a", "#f4a261", "#e76f51"],

        ["#e63946", "#f1faee", "#a8dadc", "#457b9d", "#1d3557"],

        ["#335c67", "#fff3b0", "#e09f3e", "#9e2a2b", "#540b0e"],

        ["#283d3b", "#197278", "#edddd4", "#c44536", "#772e25"],
      ],
    };
  },
  mounted() {
    this.setInitialColors();
    this.renderChart();
  },
  methods: {
    updateChartColor(index, color) {
      this.chartData[index].backgroundColor = color;
      this.updateChart();
    },
    exportData() {
      const canvas = this.$refs.myChart;
      const dataURL = canvas.toDataURL("image/png");
      const blob = this.dataURItoBlob(dataURL);
      FileSaver.saveAs(blob, "chart.png");
    },
    removeColumn(index) {
      this.chartData.splice(index, 1);
      this.updateChart();
    },
    renderChart() {
      const ctx = this.$refs.myChart.getContext("2d");
      this.chart = new Chart(ctx, {
        type: "bar",
        data: {
          labels: this.chartData.map((data) => data.label),
          datasets: [
            {
              label: "",
              data: this.chartData.map((data) => data.value),
              backgroundColor: this.chartData.map(
                (data) => data.backgroundColor
              ),
              borderColor: this.chartData.map(() => "transparent"),
              borderWidth: 1,
            },
          ],
        },
        options: {
          scales: {
            y: {
              beginAtZero: true,
            },
          },
          plugins: {
            legend: {
              display: false,
            },
          },
        },
      });
    },
    updateChart() {
      this.chart.data.datasets[0].data = this.chartData.map(
        (data) => data.value
      );
      this.chart.data.labels = this.chartData.map((data) => data.label);
      this.chart.data.datasets[0].backgroundColor = this.chartData.map(
        (data) => data.backgroundColor
      );
      this.chart.update();
    },
    addNewColumn() {
      if (this.newColumnName.trim() !== "") {
        this.chartData.push({
          label: this.newColumnName,
          value: 5,
          backgroundColor: this.newColumnColor,
        });
        this.newColumnName = "col " + (this.chartData.length + 1).toString();
        this.updateChart();
      }
    },
    setInitialColors() {
      // const usedColors = new Set();
      // this.chartData.forEach((data, index) => {
      //   let randomColorIndex;
      //   do {
      //     randomColorIndex = Math.floor(Math.random() * this.colors.length);
      //   } while (usedColors.has(randomColorIndex));
      //   usedColors.add(randomColorIndex);
      //   const randomColor = this.colors[randomColorIndex];
      //   this.chartData[index].backgroundColor = randomColor;
      // });

      this.chartData.forEach((data, index) => {
        this.chartData[index].backgroundColor =
          this.startingColors[Math.floor(Math.random() * 4)][index];
      });
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
