<template>
  <div>
    <h1>SearchBar</h1>
    <input type="text" v-model="searchSubject" @keyup.enter="search" />
  </div>
</template>

<script>
export default {
  name: "SearchBar",
  data: function () {
    return {
      searchSubject: null,
    };
  },
  methods: {
    search: function () {
      this.$emit("search", this.searchSubject);
      console.log('this', this)
      this.searchSubject = null;
    },
  },
};
</script>

<style>
</style>