<template>
  <div>
    <form>
      <label for="searchField">Search:</label>
      <input type="text" npm v-model="searchString" id="searchField">
    </form>
    <button @click="searchDb">Submit</button>
    <!-- <p>{{info}}</p> -->
    <ul v-for="movie in info" :key="movie.id">
      <li>
        <h3>{{movie.original_title}}</h3>
        <p>Overview: {{movie.overview}}</p>
        <p>Viewer rating: {{movie.vote_average}}</p>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      searchString: "",
      info: null
    };
  },
  methods: {
    searchDb() {
      let searchURL = `https://api.themoviedb.org/3/search/movie?api_key=***KEY***&query=${
        this.searchString
      }&page=1`;
      axios.get(searchURL).then(res => (this.info = res.data.results));
    }
  }
};
</script>

<style>
</style>

