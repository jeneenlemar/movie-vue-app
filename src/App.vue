<template>
  <div id="app">
    <div id="nav">
       <nav class="gtco-nav" role="navigation">
        <div class="gtco-container">
          <div class="row">
            <div class="col-sm-2 col-xs-12">
              <div id="gtco-logo"><a href="index.html">Movies!</a></div>
            </div>
            <div class="col-xs-10 text-right menu-1">
              <ul>
                <li class="active"><a href="index.html">Home</a></li>
                <li></li>
                <li><router-link  to="/movies">Movie List</router-link></li>
                <li><router-link  to="/movies/new">New Movie</router-link></li>
                <li><router-link v-if="!isLoggedIn()" to="/signup">Signup</router-link></li>
                <li><router-link v-if="!isLoggedIn()" to="/login">Login</router-link></li>
                <li><router-link v-if="isLoggedIn()" to="/logout">Logout</router-link></li>
              </ul>
            </div>
          </div>
        </div>
       </nav>
      <div class="container">
         <router-view/>
      </div>
    </div>
   <footer id="gtco-footer" class="gtco-section" role="contentinfo">
    <div class="gtco-container">
      <div class="row row-pb-md">
        <div class="col-md-4 gtco-widget gtco-footer-paragraph">
          <h3>Movies!</h3>
          <p>All you need to know about movies! </p>
        </div>
        <div class="col-md-4">
          <div class="row">
            <div class="col-md-6 gtco-footer-link">
              <h3>Links</h3>
              <ul class="gtco-list-link">
                <li><a href="#">Home</a></li>
                <li><a href="#">Features</a></li>
                <li><a href="#">Products</a></li>
                <li><a href="#">Testimonial</a></li>
                <li><a href="#">Contact</a></li>
              </ul>
            </div>
            
          </div>
        </div>
        <div class="col-md-4 gtco-footer-subscribe">
          <form class="form-inline">
            <div class="form-group">
              <label class="sr-only" for="exampleInputEmail3">Email address</label>
              <input type="email" class="form-control" id="" placeholder="Email">
            </div>
            <button type="submit" class="btn btn-primary">Send</button>
          </form>
        </div>
      </div>
    </div>
    <div class="gtco-copyright">
      <div class="gtco-container">
        <div class="row">
          <div class="col-md-6 text-left">
            <p><small>&copy; 2016 Free HTML5. All Rights Reserved. </small></p>
          </div>
          <div class="col-md-6 text-right">
            <p><small>Designed by <a href="http://freehtml5.co/" target="_blank">FreeHTML5.co</a> Demo Images: <a href="http://pixeden.com/" target="_blank">Pixeden</a> &amp; <a href="http://unsplash.com" target="_blank">Unsplash</a></small> </p>
          </div>
        </div>
      </div>
    </div>
   </footer>
  </div>
</template>

<style>

</style>
<script>

export default {
  methods: {
    isLoggedIn: function() {
      if (localStorage.getItem("jwt")) {
        return true;
      } else {
        return false;
      }
    },
    getUserId: function() {
      return localStorage.getItem("user_id");
    }
  }
};
</script>
