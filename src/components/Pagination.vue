<template>
  <div v-if="this.movies">
    <ul class="pagination pagination-lg">
      <li class="page-item disabled">
        <a class="page-link" href="#">&laquo;</a>
      </li>
      <li class="page-item active">
        <a class="page-link" href="#">1</a>
      </li>
      <li class="page-item">
        <a class="page-link" href="#">2</a>
      </li>
      <li class="page-item">
        <a class="page-link" href="#">3</a>
      </li>
      <li class="page-item">
        <a class="page-link" href="#">4</a>
      </li>
      <li class="page-item">
        <a class="page-link" href="#">5</a>
      </li>
      <li class="page-item">
        <a class="page-link" href="#" @click="nextPage">&raquo;</a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Pagination",
  props: ["movies"],
  data() {
    return {
      currentPage: 1,
      moviesOnPage: 5,
      visibleMovies: [],
      firstElOnPage: 0
    };
  },
  methods: {
    updateVisible() {
      this.firstElOnPage = this.currentPage * this.moviesOnPage;
      this.visibleMovies = this.movies.slice(
        this.firstElOnPage,
        this.firstElOnPage + this.moviesOnPage
      );
      this.$emit("pageUpdate", this.visibleMovies);
      console.log("updateVisible");
    },
    nextPage() {
      this.currentPage++;
      this.updateVisible();
    }
  },
  updated() {
    this.updateVisible();
  }
};
</script>

<style>
.pagination {
  justify-content: center;
}
</style>