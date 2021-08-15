<template>
  <div>
    <h3>{{ id }}:</h3>
    <ol>
      <li v-for="file in files" :key="file.filename">{{ file.filename }}</li>
    </ol>
  </div>
</template>

<script>
export default {
  props: {
    id: String,
    files: [],
  },
};
</script>

<style scope>
h3 {
  color: red;
}
</style>
