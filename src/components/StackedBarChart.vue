<template>
  <div
    class="bg-base-100 p-6 rounded-xl shadow-md 
           dark:bg-white/5 
           dark:backdrop-blur-md 
           dark:border dark:border-white/20 
           mb-6 h-[400px] font-[MyFont]"
  >
    <h2 class="text-lg font-semibold mb-4">
      Product Performance by Region
    </h2>

    <Bar
      :data="stackedBarData"
      :options="stackedBarOptions"
    />
  </div>
</template>

<script setup>
import { ref } from "vue";
import { Bar } from "vue-chartjs";
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

const stackedBarData = ref({
  labels: ["Q1", "Q2", "Q3", "Q4"],
  datasets: [
    {
      label: "North",
      data: [2400, 2900, 4200, 5100],
      backgroundColor: "#4635B1",
      stack: "Region",
    },
    {
      label: "South",
      data: [2400, 2900, 4200, 4655],
      backgroundColor: "#E82561",
      stack: "Region",
    },
    {
      label: "East",
      data: [2400, 2900, 4200, 5100],
      backgroundColor: "#ECE852",
      stack: "Region",
    },
    {
      label: "West",
      data: [2400, 2900, 4200, 3800],
      backgroundColor: "#FFA24C",
      stack: "Region",
    },
  ],
});

const stackedBarOptions = ref({
  responsive: true,
  maintainAspectRatio: false,

  plugins: {
    legend: {
      position: "top",
      labels: {
        color: "#64748b",
        boxWidth: 12,
        padding: 16,
        usePointStyle: true,
      },
    },
    tooltip: {
      callbacks: {
        afterLabel: function (context) {
          const datasetIndex = context.datasetIndex;
          const dataIndex = context.dataIndex;

          // نحسب مجموع كل الـ stacks في نفس العمود
          const total = context.chart.data.datasets
            .map(ds => ds.data[dataIndex])
            .reduce((a, b) => a + b, 0);

          const percentage = Math.round((context.raw / total) * 100);
          return `Contribution: ${percentage}%`;
        },
      },
    },
  },

  scales: {
    x: {
      stacked: true,
      grid: {
        display: false,
      },
      ticks: {
        color: "#64748b",
      },
    },
    y: {
      stacked: true,
      grid: {
        color: "rgba(0,0,0,0.05)",
      },
      ticks: {
        color: "#64748b",
        callback: function (value) {
          return "$" + value.toLocaleString();
        },
      },
    },
  },
});
</script>
