<template>
  <div class="modal">
    <div class="modal-content">
      <div class="modal-header">
        <h2 class="modal-title">{{ movieInfo.title }}</h2>
        <button
          type="button"
          class="close"
          data-dismiss="modal"
          aria-label="Close"
          @click="handleClose()"
        >
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">
        <div class="img-container">
          <img :src="`${this.baseURL}w500/${this.movieInfo.poster}`" alt="moviePoster`" />
        </div>
        <div class="info">
          <ul>
            <li>
              <h4>Overview</h4>
              <p>{{ this.movieInfo.overview }}</p>
            </li>
            <li>
              <h4>Genres</h4>
              <span v-for="genre in this.movieInfo.genres" :key="genre.id">{{ genre.name }}</span>
            </li>
            <li>
              <h4>Popularity</h4>
              <span>{{ this.movieInfo.popularity }}</span>
            </li>
            <li>
              <h4>Votes</h4>
              <span>{{ this.movieInfo.votes }}</span>
            </li>
            <li>
              <h4>Production countries</h4>
              <span
                v-for="country in this.movieInfo.countries"
                :key="country.iso_3166_1"
              >{{ country.name }}</span>
            </li>
            <li>
              <a :href="imbdBaseURL + this.movieInfo.id">Link to movie on imbd</a>
            </li>
          </ul>
        </div>
      </div>
      <div class="modal-footer"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "MovieDetail",
  props: ["moreInfo", "movieInfo", "baseURL", "api_key"],
  data() {
    return {
      isActive: true,
      imbdBaseURL: `https://www.themoviedb.org/movie/`
      // imbdURLPartTwo: '?api_key=',
    };
  },
  methods: {
    handleClose() {
      this.isActive = false;
      this.$emit("handleClose", this.isActive);
    }
  }
};
</script>

<style scoped>
.modal {
  display: block;
  height: 90vh;
  width: 70vw;
  left: 50%;
  transform: translateX(-50%);
  margin-top: 3vh;
  color: white;
}
.modal-title {
  position: relative;
  left: 50%;
  transform: translateX(-50%);
  font-weight: 800;
  color: green;
}
.modal-content {
  width: 100%;
  height: 100%;
}
.modal-body {
  display: flex;
}
img {
  height: 100%;
}
.img-container {
  max-height: 90%;
  max-width: 33%;
  /* padding: 5px; */
}
.info {
  background-color: rgb(47, 47, 47);
  padding: 15px;
  max-height: 90%;
  flex-grow: 1;
}
ul {
  flex-direction: column;
  align-content: center;
  max-height: 100%;
  flex-wrap: nowrap;
}
li {
  max-width: 90%;
  padding-top: 10px;
  padding-bottom: 10px;
  border-bottom: 2px dashed rgba(0, 128, 0, 0.438);
  /* flex-basis: 10%; */
}
span {
  margin-left: 10px;
}
</style>
