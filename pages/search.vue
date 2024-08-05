<script setup>
const searchTerm = useState("searchTerm", () => "");
const movies = useState(() => []);
const series = useState(() => []);
const { data } = await useFetch("/api/movies/search", {
  query: {
    searchTerm,
  },
  immediate: false,
  transform: (data) => {
    movies.value = data.movies.results;
    series.value = data.series.results;
  },
});
</script>

<template>
  <div>
    <form class="max-w-md mx-auto">
      <label
        for="default-search"
        class="mb-2 text-sm font-medium text-gray-900 sr-only dark:text-white"
        >Search</label
      >
      <div class="relative">
        <div
          class="absolute inset-y-0 start-0 flex items-center ps-3 pointer-events-none"
        >
          <svg
            class="w-4 h-4 text-gray-500 dark:text-gray-400"
            aria-hidden="true"
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 20 20"
          >
            <path
              stroke="currentColor"
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="m19 19-4-4m0-7A7 7 0 1 1 1 8a7 7 0 0 1 14 0Z"
            />
          </svg>
        </div>
        <input
          v-model="searchTerm"
          type="text"
          id="default-search"
          class="block w-full p-4 ps-10 text-sm text-gray-900 border border-gray-300 rounded-lg bg-gray-50 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          placeholder="Search Movies or TVSeries"
          required
        />
        <!-- <button
          type="submit"
          class="text-white absolute end-2.5 bottom-2.5 bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-4 py-2 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
        >
          Search
        </button> -->
      </div>
    </form>
    <div class="px-4">
      <section class="border-b border-slate-300 mb-8" v-if="movies.length">
        <h1 class="text-5xl font-extrabold dark:text-white mb-4">
          Searched Movies
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
      <section v-if="series.length">
        <h1 class="text-5xl font-extrabold dark:text-white mb-4">
          Searched Series
        </h1>
        <ul class="grid grid-cols-5 gap-4 justify-items-center">
          <li v-for="serie in series">
            <SeriesCard
              :poster_path="serie.poster_path"
              :name="serie.name"
              :overview="serie.overview"
              :first_air_date="serie.first_air_date"
              :popularity="serie.popularity"
              :item="serie"
            />
          </li>
          <br />
          <br />
          <br />
        </ul>
      </section>
      <!-- <div v-if="movies.value === undefined || series.value === undefind" class="text-center mt-16 animate-pulse">nothing to display</div> -->
    </div>
  </div>
</template>
