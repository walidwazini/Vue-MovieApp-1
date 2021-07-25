<template>
  <div class="container">
    <h1>OMDB website</h1>
    <div class="row">
      <div class="col-8">
        <input
          type="text"
          name="searchInput"
          placeholder="Enter film name"
          class="form-control"
          v-model="filmname"
        />
      </div>
      <div class="col-4">
        <button
          class="btn btn-primary"
          style="width: 100%"
          v-on:click="searchPressed"
        >
          Search
        </button>
      </div>
    </div>
    <hr />
    <!-- v-if : To bring out data on certain condition -->
    <table class="table table-bordered table-striped" v-if="movies.length > 0">
      <thead>
        <tr>
          <th></th>
          <th>Movie Info</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="movie in movies" :key="movie.imdbID" v-on:click="openPage(movie)">
          <td><img v-bind:src="movie.Poster" class="img-fluid"></td>
          <td>
            <h4>{{ movie.Title }}</h4>
            <p>{{ movie.Year }}</p>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
// @ is an alias to /src
export default {
  name: "Home",
  data() {
    return {
      filmname: "",
      movies: [],
    };
  },
  methods: {
    searchPressed: function () {
      console.log(this.filmname);
      fetch("https://www.omdbapi.com/?s=" + this.filmname + "&apikey=87d10179")
        .then(response => response.json())
        .then(data => (this.movies = data["Search"]));
    },
    openPage:function(movie){
      // movie.imdbID is the ID of the database
      this.$router.push('/detail/'+ movie.imdbID)
      //this.$router.push('/detail/' + movie.id)
    }
  }
}
</script>
<style>
  td:hover {
    cursor:pointer;
  }
</style>
