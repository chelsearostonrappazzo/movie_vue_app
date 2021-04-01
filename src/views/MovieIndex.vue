<template>
  <div class="movies-index">
    <div v-for="movie in movies" v-bind:key="movie.id">
      <h3>
        <router-link v-bind:to="`/movies/${movie.id}`">{{ movie.title }}</router-link>
        ({{ movie.year }})
      </h3>
      <p>{{ movie.plot }}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movies: [],
    };
  },
  created() {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("/api/movies").then((response) => {
        this.movies = response.data;
        console.log("all movies", this.movies);
      });
    },
  },
};
</script>
