<template>
  <div
    class="card bg-base-100 shadow 
           dark:bg-white/5 
           dark:backdrop-blur-md 
           dark:border 
           dark:border-white/20 font-[MyFont]"
  >
    <div class="card-body">
      <h2 class="card-title">Recent Activity</h2>

      <ul class="timeline timeline-vertical">
        <li v-for="(activity, i) in recentActivity" :key="i">
          
          <!-- لو رقم زوجي -->
          <template v-if="i % 2 === 0">
            <div class="timeline-start timeline-box bg-white dark:bg-white/10">
              <p class="font-semibold">{{ activity.type }}</p>
              <span class="text-xs opacity-60">{{ activity.time }}</span>
            </div>

            <div class="timeline-middle">
              <Icon
                icon="line-md:circle-filled-to-confirm-circle-filled-transition"
                class="w-5 h-5 text-primary"
              />
            </div>

            <hr class="bg-primary" />
          </template>

          <!-- لو رقم فردي -->
          <template v-else>
            <hr class="bg-primary" />

            <div class="timeline-middle">
              <Icon
                icon="line-md:circle-filled-to-confirm-circle-filled-transition"
                class="w-5 h-5 text-primary"
              />
            </div>

            <div class="timeline-end timeline-box bg-white dark:bg-white/10">
              <p class="font-semibold">{{ activity.type }}</p>
              <span class="text-xs opacity-60">{{ activity.time }}</span>
            </div>
          </template>

        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const recentActivity = ref([
  { type: "User Login", time: "10:30 AM" },
  { type: "New Order", time: "11:00 AM" },
  { type: "System Update", time: "12:00 PM" },
  { type: "User Logout", time: "01:30 PM" },
  { type: "New User Registered", time: "02:00 PM" },
]);
</script>
