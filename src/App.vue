<script>
import NavBar from './components/NavBar.vue'
import MovieList from './components/MoviesList.vue'

export default {
  name: 'App',
  components: { NavBar, MovieList }
}
</script>

<template>
  <header>
    <NavBar />
  </header>

  <main>
    <MovieList />
  </main>
</template>

<style scoped>
</style>
