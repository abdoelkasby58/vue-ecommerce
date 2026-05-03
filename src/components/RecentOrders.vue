<template>
  <div
    class="card bg-base-100 shadow dark:bg-white/5 dark:backdrop-blur-md dark:[--webkit-backdrop-filter:bulr(10px)] dark:border-white/50 font-[MyFont]"
  >
    <div class="card-body">
      <h2 class="card-title">Recent Orders</h2>
      <div class="overFlow-x-auto">
        <table class="table">
          <thead>
            <tr>
              <th>Order ID</th>
              <th>Customer</th>
              <th>Date</th>
              <th>Amount</th>
              <th>Status</th>
            </tr>
          </thead>
          <tbody>
            <tr
              v-for="(order, index) in recentOrders"
              :key="index"
              :style="`${order.status ?  'background: transparent' : 'background: #ffc80040' }`"
            >
              <td>{{ order.id }}</td>
              <td>{{ order.customer }}</td>
              <td>{{ order.date }}</td>
              <td class="text-amber-400">{{ order.amount }}</td>
              <td>
                <button
                  :class="`badge badge-${getStatusClass(order.status)}`"
                  @click="completed(order)"
                >
                  {{ order.status ?"Completed" : "isCompleted"  }}
                </button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
      <div class="card-actions justify-end mt-4">
        <button class="btn btn-primary">View All</button>
      </div>
    </div>
  </div>
</template>
<script setup>
import { ref } from "vue";

const recentOrders = ref([
  {
    id: "#12345",
    customer: "Jhon Doe",
    date: "2023-05-15",
    amount: "ksh 59.111",
    status: "Completed",
  },
  {
    id: "#12345",
    customer: "Jhon Doe",
    date: "2023-05-15",
    amount: "ksh 59.111",
    status: "Completed",
  },
  {
    id: "#12345",
    customer: "Jhon Doe",
    date: "2023-05-15",
    amount: "ksh 59.111",
    status: "Completed",
  },
  {
    id: "#12345",
    customer: "Jhon Doe",
    date: "2023-05-15",
    amount: "ksh 59.111",
    status: "Completed",
  },
  {
    id: "#12345",
    customer: "Jhon Doe",
    date: "2023-05-15",
    amount: "ksh 59.111",
    status: "Completed",
  },
]);

const completed = (order) => {
  order.status = !order.status;
};

function getStatusClass(status) {
  const statusMap = {
    Completed: "success",
    Pending: "warning",
    Cancelled: "error",
  };
  return statusMap[status] || "neutral";
}
</script>
