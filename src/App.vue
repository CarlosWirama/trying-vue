<template>
  <div id="app">
    <NavigationBar
      @searchTextChanged="onSearchTextChanged"
      @changeSorting="onChangeSorting"
      :average="average"
    />
    <main>
      <CountryList
        :countries="computedCountries"
        :selectedIndex="selectedIndex"
        :selectItem="selectItem"
        style="width: 300px"
      />
      <MapSection :latlng="(countries[selectedIndex] || {}).latlng" :countries="computedCountries"/>
    </main>
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
    countries: [],
    selectedIndex: null,
    isSortAlphabetical: true
  }),
  computed: {
    computedCountries: function() {
      const filteredCountries = this.countries.filter(({ name }) =>
        name.toLowerCase().includes(this.searchText.toLowerCase())
      );
      return this.isSortAlphabetical
        ? filteredCountries.sort((a, b) => a.name - b.name)
        : filteredCountries.sort((a, b) => b.population - a.population);
    },
    average: function() {
      if (!this.computedCountries || this.computedCountries.length === 0)
        return 0;
      const total = this.computedCountries.reduce(
        (subtotal, { population }) => subtotal + population,
        0
      );
      return total / this.computedCountries.length;
    }
  },
  methods: {
    selectItem(index) {
      if (this.selectedIndex === index) {
        this.selectedIndex = null;
      } else {
        this.selectedIndex = index;
      }
    },
    onSearchTextChanged(value) {
      this.searchText = value;
    },
    onChangeSorting(value) {
      this.isSortAlphabetical = !this.isSortAlphabetical;
    }
  },
  async created() {
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
  }
};
</script>

<style>
body {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background: #F4F4F4;
}
main {
  display: flex;
  width: 100vw;
  height: 100vh;
}
</style>
