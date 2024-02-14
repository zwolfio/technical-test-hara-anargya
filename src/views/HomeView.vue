<script>
import axios from "axios";
import SideBar from "../components/Sidebar.vue";
import Card from "../components/Card.vue";
import UserTable from "../components/Table.vue";
import UserPopup from "../components/Popup.vue";

export default {
  name: "HomeView",
  components: {
    SideBar,
    Card,
    UserTable,
    UserPopup,
  },
  data() {
    return {
      userList: [],
      selectedUser: null,
    };
  },
  created() {
    this.fetchUserList();
  },
  methods: {
    async fetchUserList() {
      try {
        const response = await axios.get(
          "https://api.slingacademy.com/v1/sample-data/users"
        );
        this.userList = response.data.users;
      } catch (error) {
        console.error("Error fetching user list:", error);
      }
    },
    showPopup(user) {
      this.selectedUser = user;
    },
    closePopup() {
      this.selectedUser = null;
    },
  },
};
</script>

<template>
  <div class="flex bg-gray-200 grid grid-cols-12">
    <div class="col-span-2">
      <SideBar :page="'dashboard'"/>
    </div>
    <div class="col-span-10">
      <div class="bg-white h-14 shadow-lg">
        <h1 class="text-lg font-bold py-3 pl-7">Conversion</h1>
      </div>
      <div class="w-full my-6">
        <Card />
      </div>
      <UserTable :userList="userList" @showPopup="showPopup" />
    </div>
    <UserPopup :selectedUser="selectedUser" @closePopup="closePopup" />
  </div>
</template>
