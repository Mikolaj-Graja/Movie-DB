<template>
  <div>
    <Search />
    <ul>
      <li></li>
    </ul>
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
    // fetch(`https://api.themoviedb.org/3/movie/${this.id}?api_key=${api_key}`)
    fetch(`https://api.themoviedb.org/3/configuration?api_key=${api_key}`)
      .then(response => response.json())
      .then(data => {
        console.log(data);
        this.searchMovie(this.keyword);
      })
      .catch(err => alert(err));
  },
  data() {
    return {
      id: 550,
      keyword: "black"
    };
  },
  methods: {
    searchMovie(keyword) {
      fetch(
        `https://api.themoviedb.org/3/search/movie?api_key=${api_key}&query=${keyword}`
      )
        .then(response => response.json())
        .then(data => console.log(data));
    }
  }
};
</script>

<style>
ul {
  list-style-type: none;
}
</style>