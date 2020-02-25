

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
      <button v-on:click="movie.showMoreDetails = !movie.showMoreDetails">Show Details</button>
      <div v-if="movie.showMoreDetails">
        <p>Year: {{ movie.year }}</p>
        <p>Plot: {{ movie.plot }}</p>
        <p>Director: {{ movie.director }}</p>
        <p>English: {{ movie.english }}</p>
        <div>
          Title:
          <input type="text" v-model="movie.title"><br>
          Year:
          <input type="text" v-model="movie.year"><br>
          Plot:
          <input type="text" v-model="movie.plot"><br>
          Director:
          <input type="text" v-model="movie.director"><br>
          English:
          <input type="text" v-model="movie.english"><br>
          <button v-on:click="updateMovie(movie)">Update Movie Info</button>
        </div> 
      </div>
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
      currentMovie: {},
      newMovieTitle: "",
      newMovieYear: "",
      newMoviePlot: "",
      newMovieDirector: "",
      newMovieEnglish: true
    };
  },
  created: function() {
    axios.get("/api/movies").then(response => {
      // this.movies = response.data;  go back and find out why this made the button not work. Did you mix Peter's way and Dani's way?  You still need to understand the WHY... you are not getting this!!!!!!
      response.data.forEach(movie => {
        movie.showMoreDetails = false;
      });
      console.log(response.data);
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
      axios.post("/api/movies", params)
        .then(response => {
          console.log("Success!", response.data);
          this.movies.push(response.data);
        })
        .catch(error => {
          console.log(error.response.data.errors);
          this.errors = error.response.data.errors;
        });
    },
    updateMovie: function(movie) {
      var params = {
        title: movie.title,
        year: movie.year,
        plot: movie.plot,
        director: movie.director,
        english: movie.english
      };
      axios.patch(`/api/movies/${movie.id}`, params).then(response => {
        console.log("Success!", response.data);
      })
        .catch(error => {
          console.log(error.response.data.errors);
        });
    }
    //   axios.post("/api/movies", params).then(response => {
    //     this.movies.push(response.data);
    //     this.newMovieTitle = "";
    //     this.newMovieYear = "";
    //     this.newMoviePlot = "";
    //     this.newMovieDirector = "";
    //     this.newMovieEnglish = "";
    //   });
    // },
  //   showMoreDetails: function(movie) {
  //     if (this.currentMovie === movie) {
  //       this.currentMovie = {};
  //     } else {
  //       this.currentMovie = movie;
  //     }
  //   }
  // }
  },
};
</script>


