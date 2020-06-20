<template>
  <div id="app">
    <Header @handleSearch="handleSearch" />
    <List :searchResult="searchResult" />
    <MadeBy />
  </div>
</template>

<script>
import List from "./components/List";
import MadeBy from "./components/MadeBy";
import Header from "./components/Header";
import api_key from "./components/API_key"; // API_key.js is in .gitignore, bacaue it is unique and cannot be seen in public

export default {
  name: "App",
  components: {
    List,
    MadeBy,
    Header
  },
  data() {
    return {
      searchResult: "",
      configuration: "w500",
      base_URL: `https://image.tmdb.org/t/p/w200`,
      keyword: ""
    };
  },
  methods: {
    handleSearch(keyword) {
      fetch(
        `https://api.themoviedb.org/3/search/movie?api_key=${api_key}&query=${keyword}`
      )
        .then(response => response.json())
        .then(data => {
          this.searchResult = data.results;
        });
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding-top: 60px;
  min-height: 100vh;
}
</style>
