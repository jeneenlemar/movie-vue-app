

<template>
  <div class="movies-show">
    <h1>{{ message }}</h1>

    <div>
      Title: {{movie.title}}<br>
      Year & Plot: {{movie.year}} - {{movie.plot}}<br>
      <router-link :to="`/movies/${movie.id}/edit`"> Edit </router-link>
     
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
      message: "Movie Information!!!",
      movie: {}
    };
  },

  created: function() {
    axios.get(`/api/movies/${this.$route.params.id}`).then(response => {
      console.log(response.data);
      this.movie = response.data;
    });
  },
  methods: {}
};
</script>
