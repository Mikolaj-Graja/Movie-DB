<template>
  <div>
    <Search />
  </div>
</template>

<script>
import Search from "./Search.vue";
import api_key from "./API_key";
export default {
  name: "List",
  props: [],
  components: {
    Search
  },
  created() {
    fetch("http://example.com/movies.json")
      .then(response => response.json())
      .then(data => console.log(data));
  },
  data() {
    key: api_key;
  }
};
</script>

<style>
</style>