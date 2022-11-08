<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <SearchBar @search="search" />
    <MainVideo />
    <VideoList />
  </div>
</template>

<script>
import SearchBar from "@/components/SearchBar.vue";
import MainVideo from "@/components/MainVideo.vue";
import VideoList from "@/components/VideoList.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    SearchBar,
    MainVideo,
    VideoList,
  },
  data: function () {
    return {};
  },
  methods: {
    search: function (searchSubject) {
      console.log("검색한 것", searchSubject);

      const API_URL = "https://www.googleapis.com/youtube/v3/videos";
      const API_KEY = process.env.VUE_APP_YOUTUBE_API_KEY;
      console.log(API_KEY);

      axios({
        method: "get",
        url: API_URL,
        params: {
          key: API_KEY,
          part: "snippet",
          type: "video",
          q: searchSubject,
        },
      }).then((response) => {
        console.log(response);
      });
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
