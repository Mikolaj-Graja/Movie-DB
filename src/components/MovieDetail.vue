<template>
  <div class="modal">
    <div class="modal-content">
      <div class="modal-header">
        <h2 class="modal-title">{{movieInfo.title}}</h2>
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
          <img :src="this.baseURL + this.movieInfo.poster" alt="moviePoster" />
        </div>
        <div class="info">
          <h4>Overview</h4>
          <p>{{this.movieInfo.overview}}</p>
          <h4>Genres</h4>
          <p>{{this.movieInfo.genres}}</p>
          <h4>Popularity</h4>
          <p>{{this.movieInfo.popularity}}</p>
          <h4>Votes</h4>
          <p>{{this.movieInfo.votes}}</p>
        </div>
      </div>
      <div class="modal-footer"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "MovieDetail",
  props: ["moreInfo", "movieInfo"],
  data() {
    return {
      baseURL: `https://image.tmdb.org/t/p/w500`,
      isActive: true
    };
  },
  methods: {
    handleClose() {
      (this.isActive = false), this.$emit("handleClose", this.isActive);
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
  max-height: 80%;
}
</style>