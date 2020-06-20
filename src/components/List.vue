<template>
  <div>
    <div class="container">
      <ul v-if="searchResult.length>0">
        <li v-for="result in searchResult" :key="result.id" class="text-white card">
          <img :src="base_URL + result.poster_path" />
          <p class="title">{{ result.title }}</p>
          <p>
            Popularity:
            <b>{{ result.popularity }}</b>
          </p>
          <p>
            Number of votes:
            <b>{{ result.vote_count }}</b>
          </p>
          <button
            class="btn btn-info"
            href="#"
            role="button"
            @click="handlemoreInfo(result.id)"
          >More Details</button>
        </li>
      </ul>
      <div v-else class="no-result">
        <div class="alert alert-dismissible alert-primary">No results for your keyword</div>
        <div class="space"></div>
      </div>
      <MovieDetail v-if="moreInfo" :movieInfo="movieInfo" @handleClose="handleChildClose" />
    </div>
  </div>
</template>

<script>
import api_key from "./API_key"; // API_key.js is in .gitignore, bacaue it is unique and cannot be seen in public
import MovieDetail from "./MovieDetail";

export default {
  name: "List",
  props: ["searchResult"],
  components: {
    MovieDetail
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
      base_URL: `https://image.tmdb.org/t/p/w200`,
      keyword: "",
      moreInfo: false,
      movieInfo: {
        overview: "",
        genres: "",
        poster: "",
        title: "",
        popularity: "",
        votes: ""
      }
    };
  },
  methods: {
    handlemoreInfo(movieId) {
      console.log(movieId);
      this.moreInfo = true;
      fetch(`https://api.themoviedb.org/3/movie/${movieId}?api_key=${api_key}`)
        .then(response => response.json())
        .then(data => {
          this.movieInfo.overview = data.overview;
          this.movieInfo.genres = data.genre_ids;
          this.movieInfo.poster = data.poster_path;
          this.movieInfo.title = data.title;
          this.movieInfo.popularity = data.popularity;
          this.movieInfo.votes = data.vote_count;
        });
    },
    handleChildClose(isActive) {
      this.moreInfo = isActive;
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
  margin-bottom: 15px;
  max-width: 200px;
}
.title {
  font-size: large;
  font-weight: 800;
  line-height: 40px;
  color: green;
}
.space {
  height: 33vh;
}
</style>
