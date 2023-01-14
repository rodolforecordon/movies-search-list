<script>
  export default {
    name: 'MovieCard',
    props: {
      key: String,
      poster: String,
      movieTitle: String,
      year: String,
      plot: String,
      actors: String,
    }
  }
</script>

<template>
  <li class="movie-card" :key="key">
    <div>
      <img :src="poster" :alt="movieTitle + ' poster'">
    </div>
    <div class="movie-info">
      <div class="movie-header">
        <h1>{{ movieTitle }}</h1>
        <span>({{ year }})</span>
      </div>
      <div class="movie-details">
        <p>{{ plot }}</p>
        <p><strong>Actors:</strong> {{ actors }}</p>
      </div>
    </div>
  </li>
</template>

<style scoped>
.movie-card {
  list-style-type: none;
  width: 100%;
  height: 200px;

  display: flex;
  padding: .5rem 0;
  border-bottom: 1px solid rgb(230, 230, 230);
}
.movie-card:last-child {
  border: none;
}
.movie-card img {
  width: 150px;
  height: 100%;
}
.movie-card h1 {
  font-size: 1.3rem;
  text-align: left;
  padding-left: 1rem;
  padding-right: .5rem;
}

.movie-info {
  width: 100%;
}
.movie-header {
  display: flex;
  align-items: center;
  justify-content: stretch;
  width: 100%;
}

.movie-info p {
  text-align: left;
  padding: .2rem 0 0 1rem;
}

.movie-details {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 150px;
}
</style>
