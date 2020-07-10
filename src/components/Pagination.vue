<template>
  <div v-if="this.movies">
    <ul class="pagination pagination-lg">
      <li class="page-item" :class="{disabled: previousDisabled}">
        <a class="page-link" href="#" @click="previousPage">&laquo;</a>
      </li>
      <li
        v-for="page in totalPages-1"
        :key="page.id"
        class="page-item"
        :class="{active: (currentPage === page)}"
      >
        <a class="page-link" href="#" @click="thisPage(page)">{{page}}</a>
      </li>
      <li class="page-item" :class="{disabled: nextDisabled}">
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
      firstElOnPage: 0,
      nextDisabled: false
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
      if (this.visibleMovies.length === 0) {
        this.nextDisabled = true;
      } else {
        this.nextDisabled = false;
      }
    },
    nextPage() {
      this.currentPage++;
      this.updateVisible();
    },
    previousPage() {
      this.currentPage--;
      this.updateVisible();
    },
    thisPage(page) {
      this.currentPage = page;
      this.updateVisible();
    }
  },
  updated() {
    this.updateVisible();
  },
  computed: {
    previousDisabled() {
      return this.currentPage <= 1 ? true : false;
    },
    totalPages() {
      return this.movies.length / this.moviesOnPage;
    }
  }
};
</script>

<style>
.pagination {
  justify-content: center;
}
</style>