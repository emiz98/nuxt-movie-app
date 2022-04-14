<template>
  <div class="relative bg-hero h-[20rem] bg-cover bg-no-repeat">
    <div
      class="h-full w-full absolute bottom-0 z-10 bg-gradient-to-r from-black to-transparent"
    ></div>
    <div class="text-white relative z-20 py-20 px-10">
      <span class="text-red-500 uppercase">Netflix Originals</span>
      <h1 class="text-5xl pb-10 md:pb-5">
        <span class="font-bold">Now</span> Streaming
      </h1>
      <a
        href="#movie-grid"
        class="bg-red-500 rounded-full transition ease-out hover:bg-red-600 px-4 py-2 font-bold"
        >View Movies</a
      >
    </div>
  </div>
</template>

<script>
export default {
  name: 'HeroMain',
}
</script>
