<template>
  <div class="home">
    <!-- <h1>{{ message }}</h1>
    <h1>Add a Movie</h1>
    Title:
    <input type="text" v-model="newMovieTitle" />
    <br />
    Year:
    <input type="text" v-model="newMovieYear" />
    <br />
    Plot:
    <input type="text" v-model="newMoviePlot" />
    <br />
    Director:
    <input type="text" v-model="newMovieDirector" />
    <br />
    English:
    <input type="text" v-model="newMovieEnglish" />
    <br />
    Genres:
    <input type="text" v-model="newMovieGenres" />
    <br />
    <button v-on:click="createMovie()">Add Movie</button> -->
    <!-- <div v-for="movie in movies" v-bind:key="movie.id">
      <h3>{{ movie.title }} ({{ movie.year }})</h3>
      <p>{{ movie.plot }}</p>
      <button v-on:click="showMovie(movie)">More Info</button>
    </div> -->
    <!-- <dialog id="movie-details">
      <form method="dialog">
        <h1>Movie Info</h1>
        <p>
          Title:
          <input type="text" v-model="currentMovie.title" />
        </p>
        <p>
          Year:
          <input type="text" v-model="currentMovie.year" />
        </p>
        <p>
          Plot:
          <input type="text" v-model="currentMovie.plot" />
        </p>
        <p>
          Director:
          <input type="text" v-model="currentMovie.director" />
        </p>
        <p>
          English:
          <input type="text" v-model="currentMovie.english" />
        </p>
        <p>
          Genres:
          <input type="text" v-model="currentMovie.genres" />
        </p>
        <button v-on:click="updateMovie(currentMovie)">Update</button>
        <button v-on:click="destroyMovie(currentMovie)">Destroy</button>

        <button>Close</button>
      </form>
    </dialog> -->
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Movies",
      movies: [],
      newMovieTitle: "",
      newMovieYear: "",
      newMoviePlot: "",
      newMovieDirector: "",
      newMovieEnglish: "",
      newMovieGenres: "",
      currentMovie: {},
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    // indexMovies: function () {
    //   axios.get("/api/movies").then((response) => {
    //     this.movies = response.data;
    //     console.log("all movies", this.movies);
    //   });
    // },
    // createMovie: function () {
    //   let params = {
    //     title: this.newMovieTitle,
    //     year: this.newMovieYear,
    //     plot: this.newMoviePlot,
    //     director: this.newMovieDirector,
    //     english: this.newMovieEnglish,
    //     genres: this.newMovieGenres,
    //   };
    //   axios
    //     .post("/api/movies", params)
    //     .then((response) => {
    //       console.log(this.movies);
    //       this.movies.push(response.data);
    //       this.newMovieTitle = "";
    //       this.newMovieYear = "";
    //       this.newMoviePlot = "";
    //       this.newMovieDirector = "";
    //       this.newMovieEnglish = "";
    //       this.newMovieGenres = "";
    //     })
    //     .catch((error) => console.log(error.response));
    // },
    // showMovie: function (movie) {
    //   console.log(movie.response);
    //   this.currentMovie = movie;
    //   document.querySelector("#movie-details").showModal();
    // },
    updateMovie: function (movie) {
      let params = {
        title: movie.title,
        year: movie.year,
        plot: movie.plot,
        director: movie.director,
        english: movie.english,
        genres: movie.genres,
      };
      axios.patch("/api/movies/" + movie.id, params).then((response) => {
        console.log("Success!", response.data);
      });
    },
    destroyMovie: function (movie) {
      axios.delete("api/movies/" + movie.id).then((response) => {
        console.log("Success!", response.data);
        let index = this.movies.indexof(movie);
        this.movies.splice(index, 1);
      });
    },
  },
};
</script>
