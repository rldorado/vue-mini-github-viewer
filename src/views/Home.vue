<template>
  <main>
    <header>
      <h1>Github Demo Project</h1>
    </header>
    <Search />
  </main>
</template>

<script>
import Search from '@/components/Search.vue'

export default {
  name: 'Home',
  components: { Search }
}
</script>