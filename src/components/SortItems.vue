<template>
  <div class="btn-group btn-group-toggle" data-toggle="buttons">
    <label class="btn btn-success" :class="{active: defaultActive}" @click="sortDefault">
      <input type="radio" name="options" id="option1" autocomplete="off" checked /> Default
    </label>
    <label class="btn btn-success" :class="{active: titleActive}" @click="sortTitle">
      <input type="radio" name="options" id="option2" autocomplete="off" /> Title
    </label>
    <label class="btn btn-success" :class="{active: popularityActive}" @click="sortPopularity">
      <input type="radio" name="options" id="option3" autocomplete="off" /> Popularity
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
      this.titleActive = true;
      this.defaultActive = false;
      this.popularityActive = false;
      this.sort();
    },
    sortPopularity() {
      this.sortWhat = "popularity";
      this.titleActive = false;
      this.defaultActive = false;
      this.popularityActive = true;
      this.sort();
    },
    sortDefault() {
      this.sortWhat = "default";
      this.titleActive = false;
      this.defaultActive = true;
      this.popularityActive = false;
      this.sort();
    },
    sort() {
      this.$emit("sort", this.sortWhat);
    }
  },
  data() {
    return {
      sortWhat: "",
      defaultActive: true,
      popularityActive: false,
      titleActive: false
    };
  }
};
</script>

<style scoped>
.btn-group-toggle {
  position: relative;
  top: -20px;
}
</style>