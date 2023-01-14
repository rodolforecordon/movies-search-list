<script>
  import axios from 'axios'
  import MovieCard from '../components/MovieCard.vue'

  export default {
    name: 'MoviesList',
    components: { MovieCard },
    async mounted() {
      await this.getMovies()
    },
    data() {
      return {
        searchTitle: '',
        searchType: '',
        searchYear: '',
        page: 1,
        totalResults: 0,
        totalPages: 0,
        errorMessage: undefined,
        movies: [],
        moviesNextPage: []
      }
    },
    methods: {
      async getMovies() {
        let url = `http://localhost:3000/movies/?title=${this.searchTitle}&type=${this.searchType}&year=${this.searchYear}&page=${this.page}`;
        const getMovies = await axios.get(url);

        this.movies = getMovies.data.moviesList
        this.totalResults = getMovies.data.totalMovies
        this.errorMessage = getMovies.data.message

        this.totalPages = Math.ceil(this.totalResults / 10)

        this.page++
        const nextPage = await axios.get(url);
        this.moviesNextPage = nextPage.data.moviesList

        console.log('movies', this.movies)
        console.log('moviesNextPage', this.moviesNextPage)
      },
      async getMoviesNextPage() {
        this.movies = [...this.movies, ...this.moviesNextPage]

        this.page++
        let url = `http://localhost:3000/movies/?title=${this.searchTitle}&type=${this.searchType}&year=${this.searchYear}&page=${this.page}`;
        const nextPage = await axios.get(url);
        this.moviesNextPage = nextPage.data.moviesList
      },
      async searchMovies() {
        this.movies = []
        this.page = 1
        this.getMovies()
      },
    },
  }
</script>

<template>
  <div class="main-container">
    <div class="search-container">
      <label for="title-search">Title: </label>
      <input
        placeholder="Blade Runner..."
        v-model.trim="searchTitle"
        type="search"
        id="title-search"
        @input="searchMovies"
      />

      <label for="">Type: </label>
      <select
        name="typeSearch"
        id="type-search"
        v-model="searchType"
        @input="searchMovies"
      >
        <option value=""></option>
        <option value="movie">Movie</option>
        <option value="series">Series</option>
        <option value="episode">Episode</option>
      </select>

      <label for="year-search">Year: </label>
      <input
        placeholder="Year"
        v-model.trim="searchYear"
        type="search"
        id="year-search"
        @input="searchMovies"
      />
    </div>
    <div class="list-container">
      <span v-if="errorMessage">{{ errorMessage }}</span>
      <ul>
        <MovieCard
          v-for="movie in movies"
          :key="movie.imdbID"
          :poster="movie.Poster"
          :movieTitle="movie.Title"
          :year="movie.Year"
          :plot="movie.DetailedInfo.Plot"
          :actors="movie.DetailedInfo.Actors"
        />
      </ul>
    </div>
    <div v-if="page < totalPages" class="load-more">
      <button @click="getMoviesNextPage">Load More</button>
    </div>
  </div>
</template>

<style>
.main-container {
  margin: 1rem auto;
  padding: 0 1rem;
  max-width: 1100px;
}

.search-container label {
  margin-left: 1rem
}
#title-search {
  width: 300px;
  padding-left: 10px;
}
#type-search {
  width: 80px;
  padding: 4px 0;
  text-align: center;
}
#year-search {
  width: 80px;
  text-align: center;
}

.list-container ul {
  all: unset;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  padding: 1rem
}

.list-container {
  padding: 2rem
}

.load-more button {
  border: 5px solid rgb(36, 113, 255);
  border-radius: 5px;
  width: 50%;
  max-width: 600px;
  padding: .5rem;
  margin-bottom: 2rem;
  font-size: 1.5rem;
  color: rgb(36, 113, 255);
  background-color: white;
  cursor: pointer;
}

.load-more button:hover {
  color: white;
  background-color: rgb(36, 113, 255);
}

.load-more button:active {
  background-color: rgb(61, 129, 255);
}
</style>
