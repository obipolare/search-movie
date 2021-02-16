<script>
  export let title, poster, type, year;
</script>

{#key (title, poster)}
  <article class="movies__block vov fade-in-down">
    <div class="movies__overlay" />
    <div class="info">
      <ul class="info__main">
        <li class="info__item">{title}</li>
        <li class="info__item">{type}</li>
        <li class="info__item">{year}</li>
      </ul>
    </div>
    <h3 class="movies__title">{title}</h3>
    <figure class="movies__figure">
      {#if poster !== "N/A"}
        <img src={poster} alt={title} />
      {/if}
    </figure>
  </article>
{/key}

<style>
  .movies__block {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    position: relative;
  }
  .movies__figure {
    margin: 0;
  }
  .movies__title {
    text-align: center;
  }
  .movies__overlay {
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    visibility: hidden;
    transition: background-color 0.2s;
    z-index: 10;
  }
  .info {
    position: absolute;
    display: none;
    z-index: 100;
    color: #f8f1f1;
    align-items: center;
  }
  .info__main {
    padding-left: 0;
  }
  .info__item {
    list-style: none;
    text-align: center;
    text-transform: capitalize;
    font-size: larger;
    font-weight: bolder;
  }
  .movies__block:hover .info {
    display: flex;
    flex-direction: column;
    justify-content: center;
  }

  .movies__block:hover .movies__overlay {
    background-color: #000;
    opacity: 0.7;
    visibility: visible;
    border-radius: 0.4rem;
  }
</style>
