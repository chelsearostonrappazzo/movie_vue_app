<template>
  <div class="container movies-new">
    <form v-on:submit.prevent="createMovie()">
      <h1>Add a Movie</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div class="form-group">
        <label>Title:</label>
        <input type="text" class="form-control" v-model="title" />
      </div>
      <div class="form-group">
        <label>Year:</label>
        <input type="text" class="form-control" v-model="year" />
      </div>
      <div class="form-group">
        <label>Plot:</label>
        <input type="text" class="form-control" v-model="plot" />
      </div>
      <div class="form-group">
        <label>Director:</label>
        <input type="text" class="form-control" v-model="director" />
      </div>
      <div class="form-group">
        <label>English:</label>
        <input type="text" class="form-control" v-model="english" />
      </div>
      <div class="form-group">
        <label>Genres:</label>
        <input type="text" class="form-control" v-model="genres" />
      </div>
      <div class="form-group">
        <label>Image:</label>
        <input type="text" class="form-control" v-model="image" />
      </div>
      <input type="submit" class="btn btn-primary" value="Submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      title: "",
      year: "",
      plot: "",
      director: "",
      english: "",
      genres: "",
      image: "",
      errors: [],
    };
  },
  created: function () {},
  methods: {
    createMovie: function () {
      let params = {
        title: this.title,
        year: this.year,
        plot: this.plot,
        director: this.director,
        english: this.english,
        genres: this.genres,
        image: this.image,
      };
      axios
        .post("/api/movies/", params)
        .then((response) => {
          console.log(this.movies);
          this.movies.push(response.data);
          this.title = "";
          this.year = "";
          this.plot = "";
          this.director = "";
          this.english = "";
          this.genres = "";
          this.image = "image";
          this.$router.push("/movies");
        })
        .catch((error) => console.log(error.response));
    },
  },
};
</script>
