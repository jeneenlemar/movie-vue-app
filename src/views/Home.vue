<template>
  <div class="home">
    <h1>New Movie</h1>
    <div>
      Title:
      <input type="text" v-model="newMovieTitle"><br>
      Year:
      <input type="text" v-model="newMovieYear"><br>
      Plot:
      <input type="text" v-model="newMoviePlot"><br>
      Director:
      <input type="text" v-model="newMovieDirector"><br>
      English (true or false):
      <input type="text" v-model="newMovieEnglish"><br>
      <button v-on:click="createMovie()">Save Movie</button>

    </div>
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
      movies: [],
      newMovieTitle: "",
      newMovieYear: "",
      newMoviePlot: "",
      newMovieDirector: "",
      newMovieEnglish: true
    };
  },
  created: function() {
    axios.get("/api/movies").then(response => {
      this.movies = response.data;
    });
  },
  methods: {
    createMovie: function() {
      var params = {
        title: this.newMovieTitle,
        year: this.newMovieYear,
        plot: this.newMoviePlot,
        director: this.newMovieDirector,
        english: this.newMovieEnglish
      };
      axios.post("/api/movies", params).then(response => {
        this.movies.push(response.data);
        this.newMovieTitle = "";
        this.newMovieYear = "";
        this.newMoviePlot = "";
        this.newMovieDirector = "";
        this.newMovieEnglish = "";
      });

    }
  }
};
</script>


