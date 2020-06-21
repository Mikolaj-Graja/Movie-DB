<template>
  <div class="btn-group btn-group-toggle" data-toggle="buttons">
    <label class="btn btn-success active" @click="sortDefault">
      <input type="radio" name="options" id="option1" autocomplete="off" checked /> Default
    </label>
    <label class="btn btn-success" :value="'name'" @click="sortTitle">
      <input type="radio" name="options" id="option2" autocomplete="off" /> Title
    </label>
    <label class="btn btn-success">
      <input type="radio" name="options" id="option3" autocomplete="off" @click="sortPopularity" /> Popularity
    </label>
  </div>
</template>

<script>
export default {
  name: "SortItems",
  // props: ["searchResult"],
  methods: {
    sortTitle() {
      this.sortWhat = "title";
      console.log("i am at sortTitle");
      this.sort();
    },
    sortPopularity() {
      this.sortWhat = "popularity";
      this.sort();
    },
    sortDefault() {
      this.sortWhat = "default";
      this.sort();
    },
    sort() {
      console.log(this.sortWhat + "I am at sort");
      // this.sortWhat = `${event.value}`;
      this.$emit("sort", this.sortWhat);
    }
  },
  data() {
    return {
      sortWhat: ""
    };
  }
};
</script>

<style scoped>
.btn-group-toggle {
  position: relative;
  top: -20px;
  /* background-color: green; */
}
</style>