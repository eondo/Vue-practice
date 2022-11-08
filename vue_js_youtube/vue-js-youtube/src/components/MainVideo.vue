<template>
  <div>
    <h1>MainVideo</h1>
    <div v-if="searchedMain">
      <iframe width="560" height="315" :src="`https://www.youtube.com/embed/${searchedMain.id.videoId}`" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
      <p>{{ searchedMain.snippet.title }}</p>
      <p>{{ searchedMain.snippet.channelTitle }}</p>
      <span>{{ searchedMain.snippet.description }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "MainVideo",
  props: {
    searchedMain: Object
  },
};
</script>

<style>
</style>