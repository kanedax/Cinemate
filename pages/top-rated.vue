<script setup>
const movies = useState(() => []);
const series = useState(() => []);

const { date } = await useFetch("/api/movies/top_rated", {
  transform: (data) => {
    movies.value = data.topRatedMovies.results;
    series.value = data.topRatedSeries.results;
  },
});
</script>

<template>
      <div class="px-4">
    <section class="border-b border-slate-300 mb-8">
      <h1 class="text-5xl font-extrabold dark:text-white mb-4">Top Rated Movies</h1>
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
        <br>
        <br>
        <br>
      </ul>
    </section>
    <section>
      <h1 class="text-5xl font-extrabold dark:text-white mb-4">Top Rated Series</h1>
      <ul class="grid grid-cols-5 gap-4 justify-items-center">
        <li v-for="serie in series" >
          <SeriesCard
            :poster_path="serie.poster_path"
            :name="serie.name"
            :overview="serie.overview"
            :first_air_date="serie.first_air_date"
            :popularity="serie.popularity"
            :item="serie"
          />
        </li>
        <br>
        <br>
        <br>
      </ul>
    </section>
  </div>
</template>
