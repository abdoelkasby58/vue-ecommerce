<template>
  <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6 font-[MyFont]">
    <!-- Animated Revenue Line Chart -->
    <div
      class="bg-base-100 p-6 rounded-xl shadow-md dark:bg-white/5 dark:backdrop-blur-md dark:[--webkit-backdrop-filter:blur(10px)] dark:border-white/20"
    >
      <h2 class="text-lg font-semibold mb-4">Monthly Revenue</h2>
      <Line
        :data="revenuChartData"
        :options="LineChartOption"
        class="max-h-[300px]"
        :key="lineChartKey"
      />
    </div>
    <!-- Animated Doughunt Chart -->
    <div
      class="bg-base-100 p-6 rounded-xl shadow-md dark:bg-white/5 dark:backdrop-blur-md dark:[--webkit-backdrop-filter:blur(10px)] dark:border-white/20"
    >
      <h2 class="text-lg font-semibold mb-4">Revenue Sources</h2>
      <Doughnut
        :data="doughnutChartData"
        :options="doughnutChartOption"
        class="max-h-[300px]"
        :key="doughnutChartKey"
      />
    </div>
  </div>
</template>
<script setup>
import { ref, onMounted } from "vue";
import { Doughnut, Line } from "vue-chartjs";
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  LineElement,
  CategoryScale,
  LinearScale,
  PointElement,
  ArcElement,
} from "chart.js";

ChartJS.register(
  Title,
  Tooltip,
  Legend,
  LineElement,
  CategoryScale,
  LinearScale,
  PointElement,
  ArcElement,
);

const lineChartKey = ref(0);
const doughnutChartKey = ref(0);

const revenuChartData = ref({
  labels: ["Jan", "Feb", "Mar", "Apr", "May", "Jun"],
  datasets: [
    {
      label: "Revenue ($)",
      data: [12000, 1900, 3000, 25000, 1000.3, 15000],
      fill: false,
      borderColor: "#E82561",
      tension: 0.4,
    },
  ],
});
const LineChartOption = ref({
  responsive: true,
  maintainAspectRatio: false,
  animations: {
    tension: {
      duration: 1000,
      easing: "linear",
      from: 1,
      to: 0,
      loop: false,
    },
  },
  plugins: {
    legend: {
      labels: {
        color: "#64748b",
      },
    },
  },
  scales: {
    x: {
      grid: {
        color: "rgba(0,0,0,0.1)",
      },
    },
  y: {
      grid: {
        color: "rgba(0,0,0,0.1)",
      },
      ticks: {
        color: "#64748b",
      },
    },
  },
});
const doughnutChartData = ref({
  labels: ["Products", "Services", "Subscription", "Consulting"],
  datasets: [
    {
      data: [115, 75, 60, 40],
      backgroundColor: ["#463581", "#E82561", "#ECE852", "#FFA24C"],
      borderWidth: 0,
      hoverOffset: 10,
    },
  ],
});
const doughnutChartOption = ref({
  responsive: true,
  maintainAspectRatio: false,
  cutout: "70%",
  animations: {
    duration: 1000,
    easing: "easeOutQuart",
    animateScale: true,
    animateRotate: true,
  },
  plugins: {
    legend: {
      position: "right",
      labels: {
        color: "#64748b",
        boxWidth: 12,
        padding: 16,
      },
    },
    tooltip: {
      callbacks: {
        label: function (context) {
          return `${context.label}:${context.raw}%`;
        },
      },
    },
  },
});
onMounted(() => {
  //Force re-render of charts to trigger animations
  lineChartKey.value++;
  doughnutChartKey.value++;
});
</script>
