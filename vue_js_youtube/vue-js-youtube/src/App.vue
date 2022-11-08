<template>
  <div id="app">
    <SearchBar @search="search" />
    <MainVideo :searched-main="searchedMain"/>
    <VideoList @go-to-main="goToMain" :searched-list="searchedList"/>
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
    return {
      searchedMain: null,
      searchedList: null,
    };
  },
  methods: {
    search: function (searchSubject) {
      console.log("검색한 것", searchSubject);

      const API_URL = "https://www.googleapis.com/youtube/v3/search";
      const API_KEY = process.env.VUE_APP_YOUTUBE_API_KEY;

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
        console.log(response); // 응답은 총 5개의 {}가 data의 items라는 배열에 들어있음 [{}, {}, {}]
        this.searchedList = response.data.items.slice(1) // 검색결과리스트에다가 response.data를 저장
        this.searchedMain = response.data.items[0]
      });
    },
    goToMain(video) {
      const newSearchedList = this.searchedList.map((searched) => {
        if (searched === video) {
          searched = this.searchedMain
        } return searched
      })
      this.searchedMain = video
      this.searchedList = newSearchedList
    }
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
