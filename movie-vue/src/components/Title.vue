<template>
  <div>
    <h1>{{titleName}}</h1>
  </div>
</template>

<script lang="ts">
export default {
  props: {
    titleName: { type: String, required: true }
  },
  data() {
    return {
      thisname: "This is not what i want"
    };
  }
};
</script>