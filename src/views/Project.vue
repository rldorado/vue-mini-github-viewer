<template>
  <main>
    <header>
      <img class="arrow" src="@/assets/img/backButton.svg" @click="goBack()" />
      <h1>{{ projectName }}</h1>
    </header>
    <div class="readme" v-html="readme" />
  </main>
</template>

<script>
import axios from "axios";

export default {
  computed: {
    projectName() {
      return this.$route.params.repo;
    }
  },
  data: () => ({
    readme: undefined
  }),
  created() {
    const name = this.$route.params.username;
    const repo = this.$route.params.repo;
    return axios
      .get(`http://api.github.com/repos/${name}/${repo}/readme`, {
        headers: { Accept: "application/vnd.github.v3.html" }
      })
      .then(response => {
        this.readme = response.data;
      });
  },
  methods: {
    goBack() {
      window.history.length > 1 ? this.$router.go(-1) : this.router.push("/");
    }
  }
};
</script>

<style scoped>
.readme {
    display: flex;
    justify-content: center;
}
</style>