<template>
  <div class="drawer lg:drawer-open font-display font-[MyFont]">
    <input type="checkbox" id="my-drawer" class="drawer-toggle" />
    <!-- Page Content -->
    <div class="drawer-content flex flex-col">
      <NavBar
        :is-dark="isDark"
        @toggle-drawer="toggleDrawer"
        @toggle-theme="toggleTheme"
      />
      <!-- Main conten -->
      <main class="flex-1 p-6 bg-base-200 dark:backgroundDark">
        <StatsCards />
        <Charts />
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
          <RecentOrders class="lg:col-span-2" />
          <RecentActivity />
        </div>
        <StackedBarChart class="mt-9" />
      </main>
    </div>
    <sidbar></sidbar>
  </div>
</template>

<script setup>
import NavBar from "@/components/NavBar.vue";
import { onMounted, ref, watchEffect } from "vue";
import Sidbar from "./components/Sidbar.vue";
import StatsCards from "./components/StatsCards.vue";
import Charts from "./components/Charts.vue";
import RecentOrders from "./components/RecentOrders.vue";
import RecentActivity from "./components/RecentActivity.vue";
import StackedBarChart from "./components/StackedBarChart.vue";
const isDark = ref(false);

onMounted(() => {
  const savedTheme = localStorage.getItem("theme");
  const systemDark = window.matchMedia("(prefers-color-scheme:dark)").matches;
  if (savedTheme) {
    isDark.value = savedTheme === "dark";
  } else if (systemDark) {
    isDark.value = true;
  }
});
watchEffect(() => {
  if (isDark.value) {
    document.documentElement.setAttribute("data-theme", "dark");
    localStorage.setItem("theme", "dark");
  } else {
    document.documentElement.setAttribute("data-theme", "light");
    localStorage.setItem("theme", "light");
  }
});
const toggleTheme = () => {
  isDark.value = !isDark.value;
};
const toggleDrawer = () => {
  const drawer = document.getElementById("my-drawer");
  if (drawer) {
    drawer.checked = !drawer.checked;
  }
};
</script>

<style scoped></style>
