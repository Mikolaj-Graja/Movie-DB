<template>
  <div class="container">
    <div class="jumbotron">
      <h1 class="display-3">Search for a movie</h1>
      <form action="submit" @submit.prevent="handleInput()">
        <input class="lead" type="text" placeholder="search" v-model="keyword" />
        <hr class="my-4" />
        <p class="lead">
          <button class="btn btn-primary btn-lg" href="#" role="button">Search</button>
        </p>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "Header",
  props: [],
  data() {
    return {
      keyword: ""
    };
  },
  methods: {
    handleInput() {
      this.$emit("handleSearch", this.keyword);
    }
  }
};
</script>

<style></style>
