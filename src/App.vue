<template>
  <div id="app">
    <List />
    <MadeBy />
  </div>
</template>

<script>
import List from "./components/List";
import MadeBy from "./components/MadeBy";

export default {
  name: "App",
  components: {
    List,
    MadeBy
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
