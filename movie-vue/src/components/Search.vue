<template>
  <form action>
    <label for="searchField">Search:</label>
    <input type="text" npm dv-model="searchString" id="searchField">
    <button @click="searchDb">Submit</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      searchString: ""
    };
  },
  methods: {
    searchDb() {
      console.log(this.searchString);
    }
  }
};
</script>

<style>
</style>

