<template>
  <form v-on:submit.prevent="fetchGitHubUser(search)" class="search">
    <input
      type="text"
      v-model="search"
      placeholder="Enter Github Username"
      :class="[ valid ? 'correct' : '' ]"
      @change="onChange"
    />
  </form>
</template>

<script>
import axios from "axios";

export default {
  data: () => ({
    valid: false,
    search: ""
  }),
  methods: {
    fetchGitHubUser(username) {
      axios.get("http://api.github.com/users/" + username).then(response => {
        this.valid = true;
        const login = response.data["login"];
        this.$router.push({ name: "User", params: { username: login } });
      });
    },
    onChange() {
      if (this.valid) {
        this.valid = false;
      }
    }
  }
};
</script>

<style scoped>
.search {
  display: flex;
  justify-content: center;
  margin: 10px;
  margin-top: 150px;
}
input {
  width: 100%;
  max-width: 770px;
  padding: 15px;
  background-color: #f5f9fc;
  border-radius: 140.62px;
  font-size: 28.12px;
  border: 2px solid white;
}
input:focus {
  outline: none;
}
input::placeholder {
  opacity: 0.3;
  color: #484848;
  letter-spacing: 0;
}
.correct {
  border: 2px solid green;
  background: #f5f9fc url("../assets/img/CheckmarkButton.svg") no-repeat right;
}
</style>