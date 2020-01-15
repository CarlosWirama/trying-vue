<template>
  <div id="list">
    <div
      class="item"
      :class="{ focused: selectedIndex === index }"
      v-for="(country, index) in countries"
      :key="country.id"
      @click="selectItem(index)"
    >
      <h4 class="item-title">{{ country.name }}</h4>
      <div class="item-details">
        <div>capital: {{ country.capital }}</div>
        <div>
          population:
          {{ country.population > 1000000
          ? `${Math.floor(country.population / 1000000)}m`
          : `${Math.floor(country.population / 1000)}k`
          }}
        </div>
      </div>
      <div
        class="item-subdetails"
      >borders: {{ country.borders.length ? country.borders.join(' ') : '-' }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CountryList",
  props: {
    countries: Array,
    selectedIndex: Number,
    selectItem: Function
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#list {
  height: 100%;
  padding-right: 8px;
  overflow: scroll;
}
.item {
  margin-bottom: 8px;
  padding: 2px 8px;
  cursor: pointer;
  text-align: left;
  border-radius: 4px;
  background-color: #fff;
  transition: 0.2s ease-in-out;
}
.item:hover {
  background-color: #DEDEDE;
  transition: 0.3s ease-in-out;
}
.item.focused {
  background-color: #BABABA;
  transition: 0.3s ease-in-out;
}
.item-title {
  margin: 0 0 4px;
}
.item-details {
  display: flex;
  font-size: 14px;
}
.item-details div {
  flex: 1;
}
.item-subdetails {
  font-size: 12px;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
