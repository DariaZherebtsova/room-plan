<template>
  <div class='legend'>
    <div
      class="legend-item"
      v-for="item in legend"
      :key="item.group_id"
    >
      <div class='legend-item__marker' :style="{ '--marker-color': item.color }"></div>
      <div class='legend-item__label'>{{item.label}}</div>
      <div class='legend-item__counter'>{{item.counter}}</div>
    </div>
    <div class="legend__chart">
      <PieChart ref="chart" />
    </div>
  </div>
</template>

<script>
import legend from "@/assets/data/legend.json";
import { Doughnut as PieChart } from "vue-chartjs";

export default {
  components: {
    PieChart,
  },
  mounted() {
    this.makeChart();
  },
  data() {
    return {
      legend: legend,
    }
  },
  methods: {
    makeChart() {
      const legendChartData = {
        labels: this.legend.map((it) => it.label),
        datasets: [
          {
            label: "Легенда",
            backgroundColor: this.legend.map(
              (legendItem) => legendItem.color
            ),
            data: this.legend.map(
              (legendItem) => legendItem.counter
            ),
          },
        ],
      };

      const options = {
        borderWidth: "10px",
        legend: {
          display: false,
        },
      };

      this.$refs.chart.renderChart(legendChartData, options);
    },
  }
}
</script>

<style scoped>
.legend {
  border-left: 1px solid var(--light-grey);
  padding: 30px 20px;
}
.legend-item {
  display: grid;
  grid-template-columns: 30px 1fr 30px;
  margin-bottom: 8px;
}
.legend-item__marker {
  width: 15px;
  height: 15px;
  border: 1px solid var(--light-grey);
  border-radius: 4px;
  background-color: var(--marker-color);
}
.legend-item__counter {
  color: var(--grey);
}
.legend__chart {
  margin-top: 50px;
}
</style>