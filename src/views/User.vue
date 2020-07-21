<template>
  <main>
    <header>
      <h1>{{ userName }}'s github</h1>
    </header>
    <div class="projects">
      <h2>Projects</h2>
      <ul v-if="projects">
        <li v-for="project in projects" :key="project.id">
          {{ project.name }}
        </li>
      </ul>
    </div>
  </main>
</template>

<script>
import axios from 'axios'

export default {
  computed: {
    userName () {
      return this.$route.params.username;
    }
  },
  data: () => ({
    projects: []
  }),
  created () {
      const name = this.$route.params.username;
      return axios.get(`http://api.github.com/users/${name}/projects`, { headers: { 'Accept': 'application/vnd.github.inertia-preview+json' } })
        .then((response) => {
          console.log(response.data)
          this.projects = response.data;
        })
  }
}
</script>

<style scoped>
.projects {
  display: flex;
  justify-content: space-around;
}
h2 {
  font-size: 35px;
  color: #484848;
}
</style>