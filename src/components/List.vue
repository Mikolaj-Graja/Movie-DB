<template>
  <div>
    <Header @handleSearch="handleSearch" />

    <div class="container">
      <ul>
        <li v-for="result in searchResult" :key="result.id" class="text-white card">
          <img :src="base_URL + result.poster_path" />
          <p class="title">{{ result.title }}</p>
          <p>Popularity: {{ result.popularity }}</p>
          <p>Number of votes: {{ result.vote_count }}</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import Header from "./Header";
import api_key from "./API_key"; // API_key.js is in .gitignore, bacaue it is unique and cannot be seen in public

export default {
  name: "List",
  props: [],
  components: {
    Header
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
      base_URL: `https://image.tmdb.org/t/p/w200`,
      keyword: ""
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
        });
    }
  }
};
</script>

<style>
ul {
  list-style-type: none;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  padding: 2px;
}
li {
  margin-bottom: 10px;
  max-width: 200px;
}
.title {
  font-size: large;
  font-weight: 800;
  line-height: 40px;
  color: green;
}
</style>
