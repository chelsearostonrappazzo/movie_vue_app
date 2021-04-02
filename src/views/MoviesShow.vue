<template>
  <div class="movies-show">
    <div class="container">
      <img v-bind:src="movie.image" alt="movie.title" />
      <h2>{{ movie.title }}</h2>
      <h3>{{ movie.director }}</h3>
      <b>
        <p v-for="genre in genres" v-bind:key="genre.id">{{ genre }}</p>
      </b>
      <p>({{ movie.year }})</p>
      <p>{{ movie.plot }}</p>
      <router-link v-bind:to="`/movies/${movie.id}/edit`">
        <button type="button" class="btn btn-primary">Edit</button>
      </router-link>
      <button v-on:click="destoryMovie(movie)" type="button" class="btn btn-primary">Delete</button>
    </div>
  </div>
</template>
<style>
img {
  float: left;
  max-width: 300px;
  max-height: 550px;
  padding: 10px;
}
</style>
<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movie: {},
    };
  },
  created: function () {
    this.showMovies();
  },
  methods: {
    showMovies: function () {
      axios.get("/api/movies/" + this.$route.params.id).then((response) => {
        console.log(response.data);
        this.movie = response.data;
      });
    },
    destroyMovie: function (movie) {
      axios.delete("/api/movies/" + movie.id).then(() => {
        console.log("Deleted!");
        this.$router.push("/movies");
      });
    },
  },
};
</script>
