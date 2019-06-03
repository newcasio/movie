<template>
  <div>
    <form>
      <label for="searchField">Search:</label>
      <input type="text" npm v-model="searchString" id="searchField">
    </form>
    <button @click="searchDb">Submit</button>
    <!-- <p>{{info}}</p> -->
    <ul v-for="movie in listOfMovies" :key="movie.id">
      <li>
        <h3 :noPage="lastPage" :firstPage="firstPage">{{movie.original_title}}</h3>
        <img :src="`http://image.tmdb.org/t/p/w185/${movie.poster_path}`">
        <p>Overview: {{movie.overview}}</p>
        <p>Viewer rating: {{movie.vote_average}}</p>
      </li>
    </ul>
    <button v-if="prevPage" @click="gotoPrevPage">Previous page</button>
    <button v-if="nextPage" @click="gotoNextPage">Next page</button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      searchString: "",
      info: null,
      resultsPage: 1,
      nextPage: false,
      prevPage: false,
      listOfMovies: null
    };
  },
  methods: {
    searchDb() {
      this.nextPage = true;

      //grab api key from env.local
      let keyMovie = process.env.VUE_APP_MOVIE_API_KEY;
      let searchURL = `https://api.themoviedb.org/3/search/movie?api_key=${keyMovie}&query=${
        this.searchString
      }&page=${this.resultsPage}`;

      //send request to movie db
      axios.get(searchURL).then(res => {
        this.info = res.data;
        this.listOfMovies = res.data.results;
      });
    },
    gotoNextPage() {
      this.resultsPage++;
      this.searchDb();
    },
    gotoPrevPage() {
      this.resultsPage--;
      this.searchDb();
    }
  },
  computed: {
    totalPages() {
      return this.info.total_pages;
    },
    lastPage() {
      if (this.resultsPage === this.totalPages) {
        this.nextPage = false;
      }
    },
    firstPage() {
      if (this.resultsPage !== 1) {
        this.prevPage = true;
      }
    }
  }
};
</script>

<style>
</style>

