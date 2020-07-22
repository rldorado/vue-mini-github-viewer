<template>
  <main>
    <header>
      <img class="arrow" src="@/assets/img/backButton.svg" @click="goBack()" />
      <h1>{{ userName }}'s github</h1>
    </header>
    <div class="repos">
      <h2>Projects</h2>
      <ul v-if="repos">
        <li
          v-for="repo in repos"
          :key="repo.id"
          @click="fetchGitHubRepository(repo)"
        >{{ repo.name }}</li>
      </ul>
    </div>
  </main>
</template>

<script>
import axios from "axios";

export default {
  computed: {
    userName() {
      return this.$route.params.username;
    }
  },
  data: () => ({
    repos: []
  }),
  created() {
    const name = this.userName;
    return axios
      .get(`http://api.github.com/users/${name}/repos`, {
        headers: { Accept: "application/vnd.github.inertia-preview+json" }
      })
      .then(response => {
        this.repos = response.data;
      });
  },
  methods: {
    fetchGitHubRepository(repo) {
      const name = this.userName;
      this.$router.push({
        name: "Project",
        params: { username: name, repo: repo.name }
      });
    },
    goBack() {
      window.history.length > 1 ? this.$router.go(-1) : this.router.push("/");
    }
  }
};
</script>

<style scoped>
.repos {
  display: flex;
  align-items: center;
  justify-content: space-around;
  flex-direction: column;
}
h2 {
  font-size: 35px;
  color: #484848;
}
ul {
  list-style-type: none;
  margin-block-start: 0;
  margin-block-end: 0;
  padding-inline-start: 0;
  background: #f5f9fc;
  box-shadow: 0 9px 28px 0 rgba(0, 0, 0, 0.28);
  border-top-left-radius: 18px;
  border-bottom-left-radius: 18px;
  height: 600px;
  overflow-y: auto;
}
li {
  font-size: 25px;
  color: #484848;
  padding: 30px;
}
li:hover {
  background: #00d586;
  color: #fff;
}
li:hover:first-of-type {
  border-top-left-radius: 18px;
}
li:hover:last-of-type {
  border-bottom-left-radius: 18px;
}
</style>