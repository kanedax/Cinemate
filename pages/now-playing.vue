<script setup>
const movies = useState(() => []);
const { data } = await useFetch("/api/movies/now_playing", {
  transform: (data) => {
    movies.value = data.nowPlayingMovies.results;
  },
});
</script>

<template>
  <div class="px-4">
    <section class="border-b border-slate-300 mb-8">
      <h1 class="text-5xl font-extrabold dark:text-white mb-4">
        Now playing movies
      </h1>
      <ul class="grid grid-cols-5 gap-4 justify-items-center">
        <li v-for="movie in movies" :key="movie.id">
          <MovieCard
            :poster_path="movie.poster_path"
            :title="movie.title"
            :id="movie.id"
            :overview="movie.overview"
            :release_date="movie.release_date"
            :popularity="movie.popularity"
            :item="movie"
          />
        </li>
        <br />
        <br />
        <br />
      </ul>
    </section>
  </div>
</template>
