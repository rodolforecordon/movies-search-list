<script>
  export default {
    name: 'SearchFields',
    props: {
      searchTitle: String,
      searchType: String,
      searchYear: String,
    },
    emits: ['update:searchTitle', 'update:searchType', 'update:searchYear', 'searchChange'],
    methods: {
      handler(emitValue, eventValue) {
        this.$emit(emitValue, eventValue)
        this.$emit('searchChange')
      }
    }
  }
</script>

<template>
  <div>
    <div class="search-container">
      <label for="title-search">Title: </label>
      <input
        placeholder="Batman..."
        type="search"
        id="title-search"
        :value="searchTitle"
        @input="handler('update:searchTitle', $event.target.value)"
      />

      <label for="">Type: </label>
      <select
        name="typeSearch"
        id="type-search"
        :value="searchType"
        @input="handler('update:searchType', $event.target.value)"
      >
        <option value=""></option>
        <option value="movie">Movie</option>
        <option value="series">Series</option>
        <option value="episode">Episode</option>
      </select>

      <label for="year-search">Year: </label>
      <input
        placeholder="Year"
        type="search"
        id="year-search"
        :value="searchYear"
        @input="handler('updatesearchYear:', $event.target.value)"
      />
    </div>
  </div>
</template>

<style>
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
</style>
