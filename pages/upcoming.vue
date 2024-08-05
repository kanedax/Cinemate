<script setup>
const movies = useState(() => []);
const { date } = await useFetch("/api/movies/upcoming", {
  transform: (data) => {
    movies.value = data.upcomingMovies.results;
  },
});

</script>

<template>
  <div class="px-4">
    <section>
      <h1 class="text-5xl font-extrabold dark:text-white mb-4">Upcoming Movies</h1>
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
      </ul>
    </section>
  </div>
</template>