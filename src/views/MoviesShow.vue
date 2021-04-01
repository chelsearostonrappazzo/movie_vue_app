<template>
  <div class="movies-show">
    <div class="container">
      <h2>{{ movie.title }}</h2>
      <h3>{{ movie.director }}</h3>
      <b>
        <p>{{ movie.genres }}</p>
      </b>
      <p>({{ movie.year }})</p>
      <p>{{ movie.plot }}</p>
      <router-link v-bind:to="`/movies/${movie.id}/edit`"><button>Edit</button></router-link>
      <button v-on:click="destroyMovie(movie)">Delete</button>
    </div>
  </div>
</template>

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
