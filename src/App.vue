<template>
  <div>
    <search-bar @enter-username="usernameWasEntered"></search-bar>
    <gists-list :entered-username="enteredUsername"></gists-list>
  </div>
</template>

<script>
import GistsList from "./components/GistsList.vue";
import SearchBar from "./components/SearchBar.vue";

export default {
  name: "App",
  data() {
    return {
      enteredUsername: "",
    };
  },
  methods: {
    usernameWasEntered(enteredUsername) {
      this.enteredUsername = enteredUsername;
    },
  },
  components: {
    GistsList,
    SearchBar,
  },
};
</script>

<style>
.container {
  margin: 2rem auto;
  max-width: 40rem;
  padding: 1rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
}

.flex-container {
  display: flex;
  justify-content: space-around;
}
</style>
