<script>
import SideBar from "../components/Sidebar.vue";
import cities from "../assets/js/city.js";
import provinces from "../assets/js/province.js";

export default {
  name: "OverView",
  components: {
    SideBar,
  },
  data() {
    return {
      provinces: provinces,
      cities: cities,
      sortOrder: "asc",
      order: "asc",
      cityId: null,
      provinceId: "",
      provinceName: null,
      citybyprovince: [],
    };
  },
  watch: {
    provinceId: {
      handler(newArray, oldArray) {
        console.log(this.provinceId);
        this.getcitybyid(this.provinceId);
      },
      deep: true,
    },
    cityId: {
      handler(newArray, oldArray) {
        console.log(this.cityId);
        this.getnamebycityid(this.cityId);
      },
      deep: true,
    },
  },
  methods: {
    getcitybyid(id) {
      console.log(id);
      console.log(this.citybyprovince);
      this.citybyprovince = this.cities.filter(
        (city) => city.provinsi_id === this.provinceId
      );
    },
    getProvinceName() {
      this.provinceName = this.getProvinceNameByCityId(parseInt(this.cityId));
    },
    getnamebycityid(id) {
      const city = this.cities.find((city) => city.id === id);
      console.log(city)
      if (city) {
        this.provinceName = this.provinces.find(
          (province) => province.id === city.provinsi_id
        );
        console.log(this.provinceName)
      }
    },
    sordbyid(order) {
      if (order === "asc") {
        this.provinces.sort((a, b) => a.id - b.id);
      } else if (order === "desc") {
        this.provinces.sort((a, b) => b.id - a.id);
      }
    },
    sortProvincesByName(order) {
      if (order === "asc") {
        this.provinces.sort((a, b) => a.name.localeCompare(b.name));
      } else if (order === "desc") {
        this.provinces.sort((a, b) => b.name.localeCompare(a.name));
      }
    },
  },
  computed: {
    sortedProvinces() {
      return [...this.provinces];
    },
  },
};
</script>

<template>
  <div class="flex bg-gray-100 grid grid-cols-12">
    <div class="col-span-2">
      <SideBar :page="'dashboard'" />
    </div>
    <div class="col-span-10 overflow-x-hidden">
      <div class="bg-white w-screen h-14 shadow-lg">
        <h1 class="text-lg font-bold py-3 pl-7">Conversion</h1>
      </div>
      <div class="container mx-auto mt-8">
        <label for="sortOrderId" class="mr-2 ml-5">Sort By Id:</label>
        <select
          v-model="sortOrder"
          id="sortOrderId"
          class="border rounded-md px-3 py-2 focus:outline-none focus:border-blue-500"
        >
          <option value="asc">1-9</option>
          <option value="desc">9-1</option>
        </select>
        <button
          @click="sordbyid(sortOrder)"
          class="bg-blue-500 text-white px-4 py-2 rounded-md ml-2 hover:bg-blue-600 focus:outline-none focus:bg-blue-600"
        >
          Terapkan
        </button>
        <label for="sortOrderName" class="mr-2 ml-5">Sort By Name:</label>
        <select
          v-model="order"
          id="sortOrderName"
          class="border rounded-md px-3 py-2 focus:outline-none focus:border-blue-500"
        >
          <option value="asc">A-Z</option>
          <option value="desc">Z-A</option>
        </select>
        <button
          @click="sortProvincesByName(order)"
          class="bg-blue-500 text-white px-4 py-2 rounded-md ml-2 hover:bg-blue-600 focus:outline-none focus:bg-blue-600"
        >
          Terapkan
        </button>
        <!-- Daftar provinsi -->
        <div class="bg-white-500 ml-3">
          <div class="container mx-auto mt-5">
            <div class="grid grid-cols-5 gap-4">
              <div
                v-for="province in sortedProvinces"
                :key="province.id"
                class="max-w-xs rounded-xl overflow-hidden shadow-xl bg-white"
              >
                <div class="p-3">
                  <img
                    :src="`https://picsum.photos/200/300?random=${province.id}`"
                    class="rounded h-52 w-80 object-cover mt-2"
                    alt=""
                  />
                  <div class="flex justify-center items-center mb-2">
                    <p class="font-bold text-md my-2 mr-2">
                      <span>{{ province.id }}.</span>{{ province.name }}
                    </p>
                  </div>
                  <p class="font-medium text-lg text-gray-500">
                    {{ province.msg }}
                  </p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <!-- Fitur pencarian kota berdasarkan id provinsi  -->
      <div class="container grid grid-cols-12 gap-10 p-4 mt-8">
        <div class="bg-white-500 col-span-6">
          <h2 class="text-lg font-bold mb-2">
            Daftar Kota Berdasarkan ID Provinsi
          </h2>
          <div class="flex items-center">
            <input
              type="number"
              v-model="provinceId"
              class="flex-1 border rounded-md px-3 py-2 mr-2 focus:outline-none focus:border-blue-500"
              placeholder="Masukkan ID Provinsi"
            />
            <button
              @click="getcitybyid(provinceId)"
              class="bg-blue-500 text-white px-4 py-2 rounded-md hover:bg-blue-600 focus:outline-none focus:bg-blue-600"
            >
              Cari
            </button>
          </div>
          <div
            v-if="citybyprovince.length > 0"
            class="bg-gray-100 rounded-md p-4 mt-4"
          >
            <p class="text-lg font-semibold mb-2">Daftar Kota:</p>
            <ul>
              <li v-for="city in citybyprovince" :key="city.id" class="mb-1">
                {{ city.name }}
              </li>
            </ul>
          </div>
          <p v-else class="text-red-500 mt-2">
            Ga ada bang
          </p>
        </div>
        <div class="col-span-6">
          <h2 class="text-lg font-bold mb-2">
            Cari Nama Provinsi Berdasarkan ID Kota
          </h2>
          <div class="flex items-center">
            <input
              type="number"
              v-model="cityId"
              class="flex-1 border rounded-md px-3 py-2 mr-2 focus:outline-none focus:border-blue-500"
              placeholder="Masukkan ID Kota"
            />
            <button
              @click="getProvinceName(cityId)"
              class="bg-blue-500 text-white px-4 py-2 rounded-md hover:bg-blue-600 focus:outline-none focus:bg-blue-600"
            >
              Cari
            </button>
          </div>

          <div v-if="provinceName !== null" class="bg-white-500 mt-1">
            <div class="container">
              <div class="rounded-xl overflow-hidden shadow-xl">
                <div class="px-6 py-4">
                  <div class="flex justify-center items-center mb-4">
                    <p class="font-bold text-xl my-2 mr-2">
                      {{ provinceName.name }}
                    </p>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <p v-else class="text-red-500 mt-2">
            Ga ada coy
          </p>
        </div>
      </div>
    </div>
  </div>
</template>
