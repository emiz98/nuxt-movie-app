<template>
  <div class="bg-black">
    <HeroMain />
    <main class="max-w-screen-lg mx-auto">
      <div
        id="movie-grid"
        class="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-4"
      >
        <div
          v-for="(movie, index) in movies"
          :key="index"
          class="m-3 md:m-5 mb-8"
        >
          <div class="relative group cursor-pointer overflow-hidden">
            <img
              :src="`https://image.tmdb.org/t/p/w300/${movie.poster_path}`"
              alt="poster"
              class="h-full object-cover rounded-lg"
            />
            <p
              class="absolute bg-red-500 p-2 text-white font-medium rounded-lg top-0 left-0"
            >
              {{ movie.vote_average }}
            </p>
            <p
              class="absolute transition-all line-clamp-6 translate-y-60 duration-200 ease-in-out group-hover:translate-y-0 rounded-lg bg-red-500 bottom-0 w-full p-2 text-white font-medium"
            >
              {{ movie.overview }}
            </p>
          </div>
          <div class="mt-2">
            <div class="text-white font-medium text-lg">
              {{ movie.title.slice(0, 20) }}
              <span v-if="movie.title.length > 20">...</span>
            </div>
            <div class="text-xs text-gray-500 mb-5">
              <span class="text-gray-400 font-medium">Released:</span>
              {{
                new Date(movie.release_date).toLocaleString('en-us', {
                  month: 'long',
                  day: 'numeric',
                  year: 'numeric',
                })
              }}
            </div>
            <NuxtLink
              class="text-white font-medium px-4 py-2 hover:bg-red-500 transition ease-out cursor-pointer border-2 border-red-500 rounded-lg"
              :to="{ name: 'movies-movieid', params: { movieid: movie.id } }"
              >More Info</NuxtLink
            >
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      movies: [],
    }
  },
  async fetch() {
    await this.getMovies()
  },

  methods: {
    async getMovies() {
      const data = axios.get(
        `https://api.themoviedb.org/3/discover/movie?api_key=${process.env.TMDB_API_KEY}&with_genres=878`
      )
      const result = await data
      result.data.results.forEach((movie) => {
        this.movies.push(movie)
      })
    },
  },
}
</script>
