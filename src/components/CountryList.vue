<template>
  <div style="padding: 0 8px">
    <h3
      v-for="country in countries"
      :key="country.id"
      @click="selectItem(country.id)"
    >{{ country.name }}</h3>
  </div>
</template>

<script>
export default {
  name: "CountryList",
  props: {
    countries: Array,
    selectItem: Function
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
