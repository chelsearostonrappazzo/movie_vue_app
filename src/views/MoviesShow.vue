<template>
  <div class="movies-show">
    <div class="container">
      <img v-bind:src="movie.image" alt="movie.title" />
      <h2>{{ movie.title }}</h2>
      <h3>{{ movie.director }}</h3>

      <p>({{ movie.year }})</p>
      <p>{{ movie.plot }}</p>
      <div id="movie comments">
        <h3>Comments</h3>
        <ol>
          <li v-for="comment in movie.comments" v-bind:key="comment.id">
            {{ comment.comment }}
          </li>
        </ol>
      </div>
      <div id="movie comments">
        <textarea id="comment" v-model="comment"></textarea>
      </div>
      <button v-on:click="addComment()" type="button" class="btn btn-primary">Add comment</button>
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
  padding: 20px;
}

#movie comments {
  margin: 0 auto;
  padding: 20px;
}

#comment {
  width: 500px;
  height: 150px;
}
</style>
<script>
import axios from "axios";

export default {
  data: function () {
    return {
      errors: [],
      movie: {},
      comment: "",
      comments: [],
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
    addComment: function () {
      let params = {
        comment: this.comment,
        movie_id: this.movie.id,
      };
      axios
        .post("/api/comments/", params)
        .then((response) => {
          this.comments.push(response.data);
          this.comment = "";
        })
        .catch((error) => console.log(error.response));
    },
  },
};
</script>
