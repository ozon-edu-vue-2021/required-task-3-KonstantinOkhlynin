/* eslint-disable prettier/prettier */
<template>
  <div id="app">
    <div @click="closePeople($event)" class="office">
      <Map />
      <SideMenu :person="this.people" :isUserOpenned="isUserOpenned" />
    </div>
  </div>
</template>

<script>
import Map from "./components/Map.vue";
import SideMenu from "./components/SideMenu.vue";
import peopleList from "@/assets/data/people.json";

export default {
  name: "App",
  data() {
    return {
      isUserOpenned: false,
      people: null,
      numid: null,
    };
  },
  methods: {
    getPeople: function (event) {
      let numId = event.target.closest(".place").getAttribute("id");
      this.people = peopleList[numId];
      this.openPeople();
    },
    closePeople: function (event) {
      if (!event.target.classList.contains("wrapper-table")) {
        this.isUserOpenned = false;
      }
    },
    openPeople: function () {
      this.isUserOpenned = true;
    },
  },
  mounted() {
    const groupPlaces = document.querySelector(".groupPlaces");
    groupPlaces.addEventListener("click", this.getPeople);
  },
  components: {
    Map,
    SideMenu,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
  background-color: #fafafa;
  padding: 24px;
  box-sizing: border-box;
}

html,
body,
#app {
  height: 100%;
}

* {
  box-sizing: border-box;
}

h3 {
  margin-top: 0px;
}

.office {
  display: grid;
  grid-template-columns: 1fr 320px;
  border-radius: 6px;
  border: 1px solid #ccd8e4;
  height: 100%;
  background: white;
  max-width: 1500px;
  margin: 0 auto;
}
</style>
