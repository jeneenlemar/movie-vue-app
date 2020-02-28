
<template>
  <div class="movies-new">
    <div class="container">
      <form v-on:submit.prevent="submit()">
        <h1>New Movie</h1>
        <ul>
          <li class="text-danger" v-for="error in errors">{{ error }}</li>
        </ul>
        <div class="form-group">
          <label>Title:</label> 
          <input type="text" class="form-control" v-model="title">
        </div>
        <div class="form-group">
          <label>Year:</label>
          <input type="test" class="form-control" v-model="year">
        </div>
        <div class="form-group">
          <label>Plot</label>
          <input type="text" class="form-control" v-model="plot"><br>
          <!-- <small>characters remaining</small> -->
          <small v-if="plot" v-bind:class="{fancy: plot.length > 3}"> {{ 20 - plot.length }} characters remaining</small>
        </div>
        <div class="form-group">
          <label>Director</label>
          <input type="text" class="form-control" v-model="director">
        </div>
        <div class="form-group">
          <label>English</label>
          <input type="boolean" class="form-control" v-model="english">
        </div>
        <input type="submit" class="btn btn-primary" value="Create Movie">
      </form>
    </div>
  </div>
</template>

<style>
  .fancy {
    color: red;
  }
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      title: "",
      year: "",
      plot: "",
      director: "",
      english: "",
      errors: []
    };
  },
  methods: {
    submit: function() {
      var params = {
        title: this.title,
        year: this.year,
        plot: this.plot,
        director: this.director,
        english: this.english

      };
      axios
        .post("/api/movies", params)
        .then(response => {
          this.$router.push("/movies");
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    }
  }
};
</script>