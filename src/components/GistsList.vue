<template>
  <h2>{{ enteredUsername }}</h2>
</template>

<script>
export default {
  props: {
    enteredUsername: String,
  },
  watch: {
    enteredUsername(newValue) {
      console.log("In GistsList.vue: ", newValue);
    },
  },
};
</script>

<style scoped></style>>
