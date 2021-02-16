<script>
  import MovieShowItem from "./MovieShowItem.svelte";
  export let category;

  $: console.log(category);
  let allMovies = [];

  const getMovies = async (name) => {
    const URL = `http://www.omdbapi.com/?s=${encodeURI(
      name.trim()
    )}&apikey=8530d10e&`;
    const res = await fetch(URL);
    const { Search } = await res.json();
    const movies = Search.map(({ Title, Poster, Year, Type }) => {
      return {
        title: Title,
        poster: Poster,
        year: Year,
        type: Type,
      };
    });

    return movies;
  };

  $: getMovies(category).then((data) => (allMovies = data));
</script>

{#key category}
  <h2 class="category vov fade-in-left">
    {category.toUpperCase()}
  </h2>
{/key}

{#if allMovies.length !== 0}
  {#each allMovies as { title, poster, type, year }}
    <MovieShowItem {title} {poster} {type} {year} />
  {/each}
{/if}

<style>
  .category {
    grid-column: span 3;
    margin-top: 1rem;
    margin-bottom: 0;
  }
  @media (max-width: 780px) {
    .category {
      grid-column: span 2;
    }
  }
  @media (max-width: 580px) {
    .category {
      grid-column: span 1;
    }
  }
</style>
