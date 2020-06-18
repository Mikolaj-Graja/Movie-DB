<template>
  <input type="text" placeholder="search" v-model="keyword" @change="handleInput()" />
</template>

<script>
export default {
  name: "Search",
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

<style>
</style>