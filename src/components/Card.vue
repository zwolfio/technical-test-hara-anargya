<script>
import { Icon } from "@iconify/vue";
export default {
  name: "Card",
  components:{
    Icon
  }
};
</script>

<template>
  <div class="grid md:grid-cols-12 mx-3 gap-3 max-[780px]:grid-rows-3">
    <div class="bg-white rounded-lg shadow-lg col-span-4 max-[780px]:row-span-1 px-7 py-5">
      <div class="flex flex-row justify-between items-center mb-4 py-2">
        <div>
          <h2 class="text-lg font-medium text-gray-500">Pending</h2>
          <h3 class="text-3xl font-bold text-gray-800 ">
            2.480,<span class="text-gray-500">30</span>
          </h3>
        </div>
        <Icon class="text-3xl text-gray-500" icon="solar:square-transfer-horizontal-broken"></Icon>
      </div>
      <div class="flex justify-between items-center pb-4">
        <div class="flex gap-2 text-md">
          <div class="flex text-green-500 items-center">
            <Icon class="rotate-45" icon="mingcute:arrow-up-fill"></Icon>
            <p class="text-green-500">2,15%</p>
          </div>
            <p class="text-gray-400">Last Month</p>
        </div>
        <div class="text-md">
          <p class="text-gray-500 font-bold text-end">View More</p>
        </div>
      </div>
    </div>
    <div class="bg-white rounded-lg shadow-lg col-span-4 max-[640px]:row-span-1 px-7 py-5">
      <div class="flex flex-row justify-between items-center mb-4 py-2">
        <div>
          <h2 class="text-lg font-medium text-gray-500">Paid</h2>
          <h3 class="text-3xl font-bold text-gray-800">
            84.310
          </h3>
        </div>
        <Icon class="text-3xl text-gray-500" icon="solar:square-transfer-horizontal-broken"></Icon>
      </div>
      <div class="flex justify-between items-center pb-4">
        <div class="flex gap-2 text-md">
          <div class="flex text-red-500 items-center">
            <Icon class="-rotate-45" icon="mingcute:arrow-down-fill"></Icon>
            <p class="text-red-500">1,10%</p>
          </div>
            <p class="text-gray-400">Last Month</p>
        </div>
        <div class="text-sm">
          <p class="text-gray-500 font-bold text-end">View More</p>
        </div>
      </div>
    </div>
    <div class="bg-white rounded-lg shadow-lg col-span-4 max-[640px]:row-span-1 px-7 py-5">
      <div class="flex flex-row justify-between items-center mb-4 py-2">
        <div>
          <h2 class="text-lg font-medium text-gray-500">Rejected</h2>
          <h3 class="text-3xl font-bold text-gray-800">
            12.115
          </h3>
        </div>
        <Icon class="text-3xl text-gray-500" icon="solar:square-transfer-horizontal-broken"></Icon>
      </div>
      <div class="flex justify-between items-center pb-4">
        <div class="flex gap-2 text-md">
          <div class="flex text-green-500 items-center">
            <Icon class="rotate-45" icon="mingcute:arrow-up-fill"></Icon>
            <p class="text-green-500">2,15%</p>
          </div>
            <p class="text-gray-400">Last Month</p>
        </div>
        <div class="text-md">
          <p class="text-gray-500 font-bold text-end">View More</p>
        </div>
      </div>
    </div>
  </div>
</template>
