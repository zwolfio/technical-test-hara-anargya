<script>
import { Icon } from "@iconify/vue";

export default {
  name: "Sidebar",
  components: {
    Icon,
  },
  methods: {
    activeLink(link){
      if (this.$route.path === link){
      return true} else {
        return false
      }
    }
  }
};
</script>

<template>
  <div class="flex bg-white h-full">
    <aside class="bg-white border-r border-gray-200 w-full">
      <div class="pt-8 pl-6">
        <h1 class="text-4xl font-extrabold">heylink.</h1>
      </div>
      <div class="pt-8 pl-6 pr-2">
        <ul class="space-y-2 text-sm font-normal">
          <router-link to="/">
            <li
              :class="{ 'rounded-md bg-blue-200': activeLink('/') }"
              class="flex py-2 text-black-600 items-center hover:bg-blue-400 rounded-md pl-1"
            >
              <Icon class="text-2xl ml-3" icon="tabler:home-stats"></Icon>
              <a href="/" class="block pl-3 py-2 w-full">Dashboard</a>
            </li>
          </router-link>
          <router-link to="/overview">
          <li
          :class="{ 'rounded-md bg-blue-200': activeLink('/overview') }"
            class="flex py-2 text-black-600 items-center hover:bg-blue-400 rounded-md pl-1"
          >
            <Icon class="text-2xl ml-3" icon="icon-park-outline:trend"></Icon>
            <a href="/" class="block pl-3 py-2 w-full">Overview</a>
          </li>
        </router-link>
        </ul>
      </div>
    </aside>
  </div>
</template>
