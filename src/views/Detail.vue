<template>
  <div class="container" v-if="movie">
    <div class="card p-3">
      <h1>{{ movie.Title }}</h1>
      <img v-bind:src="movie.Poster" />
      <p>This page is for page {{ id }}</p>
      <p>{{ movie.Year }}, Released on {{ movie.Released }}</p>
      <p>{{ movie.Genre }}</p>
      <p>Directed by {{ movie.Director }}</p>
      <p>{{ movie.Plot }}</p>
      <div class="card" v-for="rating in movie.Ratings" :key="rating.Source">
        <h6>{{ rating.Source }}</h6>
        <p>{{ rating.Value }}</p>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
//import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: "Detail",
  mounted() {
    // 1) Mounted is the first method that is going to be called after the page is loaded..
    fetch("https://www.omdbapi.com/?i=" + this.id + "&apikey=87d10179")
      .then((response) => response.json())
      .then((data) => (this.movie = data));
    // 2) In this scenario, when the page is loaded, you are going to call the second API

    // 3) Then you will get more information about the movie.. you will show it inside the UI
  },
  data() {
    return {
      id: this.$route.params.id,
      movie: null,
    };
  },
};
</script>
