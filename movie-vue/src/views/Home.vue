<template>
  <div class="home">
    <Title titleName="Movie Search"/>
    <Search/>
  </div>
</template>


<script lang="ts">
import Title from "@/components/Title.vue";
import Search from "@/components/Search.vue";

export default {
  components: { Title, Search }
};
</script>
