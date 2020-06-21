<template>
  <footer class="card">
    <p>
      Website made by
      <a href="https://github.com/Mikolaj-Graja">Mikołaj Graja</a>
    </p>
    <p>
      Movie data from
      <a href="https://www.themoviedb.org/">https://www.themoviedb.org/</a>
    </p>
  </footer>
</template>

<script>
export default {
  name: "MadeBy"
};
</script>

<style>
footer {
  /* display: flex; */
  /* padding-top: 10px; */
  position: relative;
  color: green;
  font-style: italic;
  font-weight: 300;
  height: 12vh;
  justify-content: space-evenly;
  padding: 0;
  margin: 0;
}
footer p {
  margin: 0;
  padding: 0;
}
</style>
