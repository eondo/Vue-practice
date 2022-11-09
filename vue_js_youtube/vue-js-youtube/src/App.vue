<template>
  <div id="app">
    <nav class="navbar navbar-light bg-light justify-content-between">
      <a class="navbar-brand" href="#">
        <img
          src="/docs/4.0/assets/brand/bootstrap-solid.svg"
          width="30"
          height="30"
          class="d-inline-block align-top"
          alt=""
        />
        Bootstrap
      </a>
      <form class="form-inline">
        <input
          class="form-control mr-sm-2"
          type="search"
          placeholder="Search"
          aria-label="Search"
        />
        <button class="btn btn-outline-success my-2 my-sm-0" type="submit">
          Search
        </button>
      </form>
    </nav>
    <SearchBar @search="search" />
    <MainVideo :searched-main="searchedMain" />
    <VideoList @go-to-main="goToMain" :searched-list="searchedList" />
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
          maxResults: 10,
        },
      }).then((response) => {
        console.log(response); // 응답은 총 5개의 {}가 data의 items라는 배열에 들어있음 [{}, {}, {}]
        this.searchedList = response.data.items.slice(1); // 검색결과리스트에다가 response.data를 저장
        this.searchedMain = response.data.items[0];
      });
    },
    goToMain(video) {
      const newSearchedList = this.searchedList.map((searched) => {
        if (searched === video) {
          searched = this.searchedMain;
        }
        return searched;
      });
      this.searchedMain = video;
      this.searchedList = newSearchedList;
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
