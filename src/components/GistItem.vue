<template>
  <div>
    <h3>Gist id <span>{{ id }}</span> :</h3>
    <gist-file
      v-for="file in files"
      :key="file.filename"
      :language="file.language"
      :filename="file.filename"
      :content-url="file.raw_url"
      >{{ file.filename }}</gist-file
    >
    <p v-if="usersWhoForked !== ''">
      The last 3 users who forked it: {{ usersWhoForked }}
    </p>
  </div>
</template>

<script>
import GistFile from "./GistFile.vue";

export default {
  props: {
    id: String,
    files: Object,
  },
  data() {
    return {
      usersWhoForked: "",
      forks: [],
    };
  },
  methods: {
    fetchForks() {
      const axios = require("axios");
      axios
        .get("https://api.github.com/gists/" + this.id + "/forks")
        .then((response) => {
          if (response.data) {
            this.forks = response.data;
            this.computeLastForksUsers();
          }
        })
        .catch((error) => {
          console.log(error);
        });
    },
    computeLastForksUsers() {
      this.forks = this.forks.reverse();
      var necessaryNumberOfForks = 0;
      var users = [];
      for (
        var i = 0;
        i < this.forks.length && necessaryNumberOfForks < 3;
        i++
      ) {
        users.push(this.forks[i].owner.login);
        necessaryNumberOfForks++;
      }
      var usersStringValue = "";
      for (var j = 0; j < users.length - 1; j++) {
        usersStringValue += users[j] + ", ";
      }

      if (users.length - 1 >= 0) {
        usersStringValue += users[users.length - 1];
      }

      this.usersWhoForked = usersStringValue;
    },
  },
  components: {
    GistFile,
  },
  created() {
    this.fetchForks();
  },
};
</script>

<style scope>
span {
  color: red;
}
</style>
