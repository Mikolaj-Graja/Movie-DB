<template>
  <div>
    <Search @handleSearch="handleSearch" />
    <ul>
      <li v-for="result in searchResult" :key="result.id">
        {{ result.title }}
        <img :src="base_URL + result.poster_path" />
      </li>
    </ul>
  </div>
</template>

<script>
import Search from "./Search";
import api_key from "./API_key"; // API_key.js is in .gitignore, bacaue it is unique and cannot be seen in public
export default {
  name: "List",
  props: [],
  components: {
    Search
  },
  created() {
    fetch(`https://api.themoviedb.org/3/configuration?api_key=${api_key}`)
      .then(response => response.json())
      .then(data => {
        console.log(data);
      })
      .catch(err => alert(err));
  },
  data() {
    return {
      searchResult: "",
      configuration: "w500",
      // result: "",
      base_URL: `https://image.tmdb.org/t/p/w200`

      // https://image.tmdb.org/t/p/w500/kqjL17yufvn9OVLyXYpvtyrFfak.jpg
    };
  },
  methods: {
    handleSearch(keyword) {
      console.log(keyword);
      fetch(
        `https://api.themoviedb.org/3/search/movie?api_key=${api_key}&query=${keyword}`
      )
        .then(response => response.json())
        .then(data => {
          this.searchResult = data.results;
          // console.log(this.searchResult);
        });
    }
  }
};
</script>

<style>
ul {
  list-style-type: none;
}
</style>
