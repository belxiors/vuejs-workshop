<template>
  <h1>Movie Characters</h1>
  <ul v-if="movies.length > 0">
    <li v-for="movie in movies" :key="movie.id">
      <div>
        <h2>{{ movie.title }}</h2>
        <button v-on:click="() => addToFavorites(movie)">Favorite!</button>
      </div>
      <ul>
        <li v-for="character in movie.characters" :key="character">{{ character }}</li>
      </ul>
    </li>
  </ul>
  <p v-else>No movies available</p>
  <h2>Favorite Movies</h2>
  <ul v-if="favoriteMovies.length > 0">
    <li v-for="movie in favoriteMovies" :key="movie.id">
      <p>{{ movie.title }}</p>
      <button v-on:click="() => removeFromFavorites(movie)">Remove</button>
    </li>
  </ul>
  <p v-else>No favorites yet</p>
</template>
<script>
export default {
  data() {
    return {
      favoriteMovies: [],
      movies: [
        {
          id: '963df132-5b53-41ce-9459-c9be81a48022',
          title: 'Inception',
          characters: ['Cobb', 'Ariadne', 'Mal']
        },
        {
          title: 'The Dark Knight',
          characters: ['Batman', 'Joker', 'Bane']
        },
        {
          id: '46994b96-5b9d-4669-8660-f020b1442a9b',
          title: 'Interstellar',
          characters: ['Cooper', 'Murph', 'Brand']
        },
        {
          id: '0ccec8e3-ff20-4e9a-8b7b-5d27cd28afd9',
          title: 'The Prestige',
          characters: ['Angier', 'Borden', 'Olivia']
        }
      ]
    }
  },
  methods: {
    addToFavorites(movie) {
      this.favoriteMovies.push(movie)
    },
    removeFromFavorites(movie) {
      this.favoriteMovies = this.favoriteMovies.filter(favMovie => favMovie.id !== movie.id)
    }
  }
}
</script>
