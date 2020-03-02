

<template>
  <div class="movies-index">

    <!-- begin pasted info section -->
    <div class="gtco-section">
      <div class="gtco-container">
        <div class="row">
          <div class="col-md-8 col-md-offset-2 gtco-heading text-center">
            <h2>Movie List</h2>
            <p>See the movies below!</p>
          </div>
        </div>
        <div class="row">

          <div class="col-md-12">
            <div class="owl-carousel owl-carousel-carousel">
              <div class="item">
                <div class="gtco-item">
                  <a href="#"><img src="images/img_1.jpg" alt="" class="img-responsive" ></a> 
                  <h2><a href="#">New York Arena</a></h2> 
                  <p class="role">New York</p>
                </div>
              </div>
              <div class="item">
                <div class="gtco-item">
                  <a href="#"><img src="images/img_2.jpg" alt="" class="img-responsive"></a>
                  <h2><a href="#">Eagle Park</a></h2>
                  <p class="role">London</p>
                </div>
              </div>
              <div class="item">
                <div class="gtco-item">
                  <a href="#"><img src="images/img_3.jpg" alt="" class="img-responsive"></a>
                  <h2><a href="#">Nationals Park</a></h2>
                  <p class="role">Paris, France</p>
                </div>
              </div>

              <div class="item">
                <div class="gtco-item">
                  <a href="#"><img src="images/img_1.jpg" alt="" class="img-responsive"></a>
                  <h2><a href="#">New York Arena</a></h2>
                  <p class="role">New York</p>
                </div>
              </div>
              <div class="item">
                <div class="gtco-item">
                  <a href="#"><img src="images/img_2.jpg" alt="" class="img-responsive"></a>
                  <h2><a href="#">Eagle Park</a></h2>
                  <p class="role">London</p>
                </div>
              </div>
              <div class="item">
                <div class="gtco-item">
                  <a href="#"><img src="images/img_3.jpg" alt="" class="img-responsive"></a>
                  <h2><a href="#">Nationals Park</a></h2>
                  <p class="role">Paris, France</p>
                </div>
              </div>

              <div class="item">
                <div class="gtco-item">
                  <a href="#"><img src="images/img_1.jpg" alt="" class="img-responsive"></a>
                  <h2><a href="#">New York Arena</a></h2>
                  <p class="role">New York</p>
                </div>
              </div>
              <div class="item">
                <div class="gtco-item">
                  <a href="#"><img src="images/img_2.jpg" alt="" class="img-responsive"></a>
                  <h2><a href="#">Eagle Park</a></h2>
                  <p class="role">London</p>
                </div>
              </div>
              <div class="item">
                <div class="gtco-item">
                  <a href="#"><img src="images/img_3.jpg" alt="" class="img-responsive"></a>
                  <h2><a href="#">Nationals Park</a></h2>
                  <p class="role">Paris, France</p>
                </div>
              </div>
            </div>
          </div>
          
        </div>
      </div>
    </div>
    <!-- end pasted info section -->
    
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
/*.selected {
  color: white;
  background-color: grey;
  
}*/
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
