<template>
  <search-bar @enter-username="usernameEntered"></search-bar>
  <gists-list :entered-username="username"></gists-list>
</template>

<script>
import GistsList from "./components/GistsList.vue";
import SearchBar from "./components/SearchBar.vue";

export default {
  name: "App",
  data() {
    return {
      username: ''
    }
  },
  methods: {
    usernameEntered(username) {
      this.username = username;
    }
  },
  components: {
    GistsList,
    SearchBar,
  },
};
</script>

<style></style>
