<template>
  <div id="app">
    <NavigationBar v-bind:searchText="searchText" :onSearchTextChanged="onSearchTextChanged"/>
    <div style="display: flex">
      <CountryList v-bind:countries="countries" :selectItem="selectItem"/>
      <MapSection msg="countries[0]" v-bind:sources="countries[0]" style="flex: 1"/>
    </div>
  </div>
</template>

<script>
import NavigationBar from "./components/NavigationBar";
import CountryList from "./components/CountryList";
import MapSection from "./components/MapSection";

export default {
  name: "App",
  components: {
    NavigationBar,
    CountryList,
    MapSection
  },
  data: () => ({
    searchText: "",
    countries: [{ id: 1, name: "singapore" }, { id: 3, name: "bangladesh" }],
    selectedIndex: null
  }),
  methods: {
    selectItem: e => console.log("e", e),
    onSearchTextChanged: () => {}
  },
  async created() {
    // fetch the data when the view is created and the data is
    // already being observed
    const countries = await fetch(
      "https://restcountries-v1.p.mashape.com/all",
      {
        headers: {
          "X-Mashape-Key": "l5eMXwY6d3mshmvnljsx6GVH9YWxp1IsKhsjsnSAZ5yXpYiGRl"
        }
      }
    ).then(r => r.json());
    if (Array.isArray(countries)) {
      this.countries = countries;
    }
    console.log(countries[0]);
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
