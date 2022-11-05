<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <SearchBar/>
    <MainVideo/>
    <VideoList/>
  </div>
</template>

<script>
import SearchBar from '@/components/SearchBar.vue'
import MainVideo from '@/components/MainVideo.vue'
import VideoList from '@/components/VideoList.vue'


export default {
  name: 'App',
  components: {
    SearchBar,
    MainVideo,
    VideoList,
  }
}
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
