<template>
  <div>
    <div class="flex">
      <button class="badge">{{ language }}</button>
      <span @click="toggleShowContent">{{ filenameWithoutExtension }}</span>
    </div>
    <div v-if="showContent">
      {{ content }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    filename: String,
    language: String,
    contentUrl: String,
  },
  data() {
    return {
      showContent: false,
      content: "",
    };
  },
  computed: {
    filenameWithoutExtension() {
      return this.filename.split(".")[0];
    },
  },
  methods: {
    toggleShowContent() {
      this.showContent = !this.showContent;
    },
    getContent() {
      const axios = require('axios');
      axios
        .get(this.contentUrl)
        .then((response) => {
          if (response.data) {
            this.content = response.data;
          }
        })
        .catch((error) => {
          console.log(
            "The following error occurred when trying to get the content for the filename ",
            this.filename,
            error
          );
        });
    },
  },
  watch: {
    showContent(newValue) {
      if (newValue === true) {
        this.getContent();
      }
    },
  },
};
</script>

<style scoped>
.flex {
  display: flex;
  justify-content: space-between;
  width: 70%;
  margin: 0.5rem;
}

.badge {
  color: white;
  background-color: blue;
  padding: 0.5rem 2rem;
  border: 1px;
  border-color: blue;
}

span {
  padding: 0.5rem 2rem;
  color: black;
}
</style>
