<script>
  import MovieShow from "./MovieShow.svelte";
  export let categories;
  let inputValue = "";

  const handleInputChange = ({ target: { value } }) => {
    inputValue = value;
  };
  const handleSubmit = (e) => {
    e.preventDefault();
    if (inputValue.trim().length > 2)
      return (categories = [inputValue, ...categories]) && (inputValue = "");
  };
</script>

<fieldset class="field">
  <legend class="field__legend">Search your Movie!</legend>
  <form class="field__form" on:submit={handleSubmit}>
    <input
      class="field__inputChange"
      type="text"
      value={inputValue}
      on:input={handleInputChange}
    />
  </form>
</fieldset>

{#each categories as category}
  <section class="movies">
    <MovieShow {category} />
  </section>
{/each}

<style>
  .movies {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1rem 2rem;
  }
  .field {
    padding-top: 1rem;
    padding-bottom: 1rem;
  }
  .field__legend {
    font-size: 2rem;
    font-weight: bold;
  }
  .field__inputChange {
    font-size: 1.04rem;
    font-weight: 400;
    width: 100%;
  }
  @media (max-width: 780px) {
    .movies {
      grid-template-columns: repeat(2, 1fr);
    }
  }
  @media (max-width: 580px) {
    .movies {
      grid-template-columns: repeat(1, 1fr);
    }
  }
</style>
