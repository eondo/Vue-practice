<template>
  <div>
    <div style="display: flex;">
      <img @click="goToMain" :src="video.snippet.thumbnails.default.url" alt="#">
      <p>{{ video.snippet.title }}</p>
    </div>
    <hr>

  </div>
</template>

<script>
export default {
  name: "VideoListItem",
  props: {
    video: Object,
  },
  methods: {
    goToMain() {
      this.$emit('go-to-main', this.video)
    }
  }
};
</script>

<style>
</style>