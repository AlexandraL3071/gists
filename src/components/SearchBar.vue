<template>
  <section>
    <div class="container">
      <form @submit.prevent="enterUsername">
        <div class="flex-container">
          <input
            type="text"
            placeholder="Enter a username..."
            id="username"
            name="username"
            ref="usernameInput"
          />
          <button type="submit">Find gists</button>
        </div>
      </form>
    </div>
  </section>
</template>

<script>
export default {
  emits: ["enterUsername"],
  data() {
    return {
      enteredUsername: "",
    };
  },
  methods: {
    enterUsername() {
      this.enteredUsername = this.$refs.usernameInput.value;
      this.$emit("enterUsername", this.enteredUsername);
    },
  },
};
</script>

<style scoped>
.form {
  align-self: center;
}

input[type="text"] {
  display: block;
  width: 20rem;
  margin-top: 0.5rem;
}

button {
  font: inherit;
  border: 1px solid #0000ff;
  background-color: #0000ff;
  color: white;
  padding: 0.5rem 2rem;
  cursor: pointer;
}

button:hover,
button:active {
  background-color: #3333ff;
  border-color: #3333ff;
}
</style>
