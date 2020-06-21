<template>
  <div>
    <SortItems v-if="searchResult.length > 0" :searchResult="this.searchResult" @sort="sort"></SortItems>
    <div class="container">
      <ul v-if="searchResult.length > 0">
        <li v-for="result in this.currentPageMovies" :key="result.id" class="text-white card">
          <img :src="base_URL + configuration + result.poster_path" />
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
      <Pagination :movies="this.movies" @pageUpdate="pageUpdate" />
      <MovieDetail
        v-if="moreInfo"
        :movieInfo="movieInfo"
        :baseURL="base_URL"
        :api_key="api_key"
        @handleClose="handleChildClose"
      />
    </div>
  </div>
</template>

<script>
import api_key from "./API_key"; // API_key.js is in .gitignore, bacaue it is unique and cannot be seen in public
import MovieDetail from "./MovieDetail";
import SortItems from "./SortItems";
import Pagination from "./Pagination";

export default {
  name: "List",
  props: ["searchResult"],
  components: {
    MovieDetail,
    SortItems,
    Pagination
  },
  data() {
    return {
      base_URL: `https://image.tmdb.org/t/p/`,
      keyword: "",
      moreInfo: false,
      api_key: api_key,
      configuration: "w200/",
      sortWhat: "default",
      sorted: "",
      currentPageMovies: [],
      movieInfo: {
        overview: "",
        genres: "",
        poster: "",
        title: "",
        popularity: "",
        votes: "",
        companies: "",
        id: "",
        homepage: ""
      }
    };
  },
  methods: {
    handlemoreInfo(movieId) {
      this.moreInfo = true;
      fetch(`https://api.themoviedb.org/3/movie/${movieId}?api_key=${api_key}`)
        .then(response => response.json())
        .then(data => {
          this.movieInfo.overview = data.overview;
          this.movieInfo.genres = data.genres;
          this.movieInfo.poster = data.poster_path;
          this.movieInfo.title = data.title;
          this.movieInfo.popularity = data.popularity;
          this.movieInfo.votes = data.vote_count;
          this.movieInfo.countries = data.production_countries;
          this.movieInfo.id = data.id;
          this.movieInfo.homepage = data.homepage;
        });
    },
    handleChildClose(isActive) {
      this.moreInfo = isActive;
    },
    sort(event) {
      this.sortWhat = event;
      this.sorted = [...this.searchResult].sort((el1, el2) => {
        if (this.sortWhat == "popularity") {
          return el1.popularity > el2.popularity ? -1 : 1;
        } else if (this.sortWhat == "title") {
          return el1.title > el2.title ? 1 : -1;
        } else {
          return this.searchResult;
        }
      });
    },
    pageUpdate(visibleMovies) {
      this.currentPageMovies = visibleMovies;
    }
  },
  computed: {
    movies() {
      return this.sortWhat === "default" ? this.searchResult : this.sorted;
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
