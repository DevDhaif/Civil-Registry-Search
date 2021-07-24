<template>
  <div class="container relative flex items-center flex-col">
    <!-- search section-->
    <div class="hello m-10 w-8/12">
      <div class="bg-white flex items-center rounded-full shadow-xl">
        <input
          type="text"
          v-model="search"
          placeholder="Search by name or id or NID "
          class="
            rounded-md
            w-full
            py-4
            px-6
            text-gray-700
            leading-tight
            focus:outline-none
            placeholder-gray-400
          "
        />
      </div>
      <div
        class="bg-blue-200 grid grid-rows-1 rounded-sm grid-cols-9 gap-4 mt-4"
      >
        <div>id</div>
        <div>name</div>
        <div>nid</div>
        <div>gender</div>
        <div>state</div>
        <div>cureent state</div>
        <div>religion</div>
        <div>blaceof birth</div>
        <div>date of birth</div>
      </div>
    </div>
    <div v-for="citizen in filterdCitizens" :key="citizen.index" class="w-8/12">
      <div
        class="bg-indigo-100 grid grid-rows-1 rounded-sm grid-cols-9 gap-2 mt-2"
      >
        <div>{{ citizen.id }}</div>
        <div>{{ citizen.fullName }}</div>
        <div>{{ citizen.nid }}</div>
        <div>{{ citizen.gender }}</div>
        <div>{{ citizen.state }}</div>
        <div>{{ citizen.currentState }}</div>
        <div>{{ citizen.religion }}</div>
        <div>{{ citizen.placeOfBirth }}</div>
        <div>{{ citizen.dateOfBirth }}</div>
      </div>
    </div>
  </div>
</template>

//
<script>
import axios from "axios";
export default {
  name: "App.vue",
  props: {
    msg: String,
  },
  data() {
    return {
      citizens: [],
      search: "",
    };
  },
  mounted() {
    axios
      .get("http://shrouded-meadow-15080.herokuapp.com/api/citizen")
      .then((response) => {
        this.citizens = response.data.data;
      });
  },
  computed: {
    filterdCitizens() {
      return this.citizens.filter((citizen) => {
        return (
          citizen.fullName.toLowerCase().includes(this.search.toLowerCase()) ||
          citizen.id == this.search ||
          citizen.nid == this.search
        );
      });
    },
  },
};
</script>
