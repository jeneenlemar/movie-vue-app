

<template>
  <div class="movies-index">
    
    <h1>{{ message }}</h1>
    <div v-for="movie in movies" v-on:click="currentMovie = movie" v-bind:class="{ selected: movie === currentMovie }">
      Title: {{movie.title}}<br>
      Year {{movie.year}} <br>
      <router-link :to="`/movies/${movie.id}`">See Details</router-link>
      <p>--</p> 
    </div>
      
  </div>
</template>

<style>
.selected {
  color: white;
  background-color: grey;
  
}
</style>

<script>
import axios from 'axios';
export default {
  data: function() {
    return {
      message: "Movie List",
      movies: [],
      currentMovie: {}
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
