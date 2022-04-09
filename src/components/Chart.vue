<template>
  <div>
    <Bar :chart-id="chartId" :dataset-id-key="chartId" :chart-options="chartOptions" :chart-data="chartData" :height="150" />
  </div>
</template>

<script>
import { Bar } from "vue-chartjs/legacy";

import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale,
} from "chart.js";

ChartJS.register(
  Title,
  Tooltip,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale
);

export default {
  props: ["chartData", "chartId"],
  data: () => ({
    chartOptions: {
      responsive: true,
    },
  }),
  components: { Bar }
};
</script>