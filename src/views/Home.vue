<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h1>All Movies</h1>
    <div v-for="movie in movies">
      <h2>{{movie.title}}</h2>
      
    </div>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      message: "Movie App!",
      movies: []
    };
  },
  created: function() {
    axios.get("/api/movies").then(response => {
      this.movies = response.data;
    });
  },
  methods: {}
};
</script>


