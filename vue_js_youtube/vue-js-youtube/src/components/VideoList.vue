<template>
  <div>
    <h1>VideoList</h1>
    <VideoListItem @go-to-main="goToMain" v-for="(video, index) in searchedList" :key="index" :video="video"/>
  </div>
</template>

<script>
import VideoListItem from "@/components/VideoListItem";

export default {
  name: "VideoList",
  components: {
    VideoListItem,
  },
  props: {
    searchedList: Array,
  },
  methods: {
    goToMain(video) {
      this.$emit('go-to-main', video)
    }
  }
};
</script>

<style>
</style>