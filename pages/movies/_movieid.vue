<template>
  <div
    v-if="$fetchState.pending"
    class="h-screen flex items-center justify-center bg-black"
  >
    <Loading />
  </div>
  <div v-else class="bg-black min-h-screen">
    <div class="text-white p-5 md:p-20 max-w-screen-lg mx-auto">
      <NuxtLink
        class="bg-red-500 hover:bg-red-600 transition ease-out px-5 py-2 rounded-md"
        :to="{ name: 'index' }"
        >Back</NuxtLink
      >
      <div class="mt-10 flex flex-col md:flex-row md:space-x-10">
        <img
          :src="`https://image.tmdb.org/t/p/w300/${movie.poster_path}`"
          alt="poster"
          class="h-60 md:h-full object-cover rounded-lg"
        />
        <div>
          <h1 class="text-2xl font-bold">{{ movie.title }}</h1>
          <p class="text-gray-400 text-sm mb-2">{{ movie.tagline }}</p>
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
          <p><span>Duration: </span>{{ movie.runtime }} minutes</p>
          <p>
            <span>Revenue: </span>
            {{
              movie.revenue.toLocaleString('en-us', {
                style: 'currency',
                currency: 'USD',
              })
            }}
          </p>
          <p class="mt-5 font-light">
            <span>Overview: </span> {{ movie.overview }}
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
const apiKey = process.env.TMDB_API_KEY
export default {
  name: 'single-movie',
  data() {
    return {
      movie: '',
    }
  },
  async fetch() {
    await this.getSingleMovie()
  },
  fetchDelay: 1000,
  head() {
    return {
      title: this.movie.title,
    }
  },
  methods: {
    async getSingleMovie() {
      const data = axios.get(
        `https://api.themoviedb.org/3/movie/${this.$route.params.movieid}?api_key=${apiKey}&language=en-US`
      )
      const result = await data
      this.movie = result.data
    },
  },
}
</script>
