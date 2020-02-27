

<template>
  <div class="movies-index">
    
    <h1>{{ message }}</h1>
    <div v-for="movie in movies">
      Title: {{movie.title}}<br>
      Year {{movie.year}} <br>
      <router-link :to="`/movies/${movie.id}`">See Details</router-link>
      <p>--</p> 
    </div>
      
  </div>
</template>

<style>
</style>

<script>
import axios from 'axios';
export default {
  data: function() {
    return {
      message: "Movie List",
      movies: []
    };
  },
  created: function() {
    axios.get("/api/movies").then(response =>{
      console.log(response.data);
      this.movies = response.data;
    });
  },
  methods: {}
};
</script>
