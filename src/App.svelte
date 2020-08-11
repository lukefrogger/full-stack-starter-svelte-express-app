<script>
  export let name;
  let gifs = [];
  let searchTerm = "";

  async function searchForGif(e) {
    try {
      const returnValue = await fetch(`/giphy?term=${searchTerm}`);
      const response = await returnValue.json();
      gifs = response.data;
    } catch (error) {
      console.error(error);
    }
  }
</script>

<style>
  .gifs-grid {
    display: grid;
    grid-gap: 10px;
    grid-template-columns: repeat(5, 1fr);
  }

  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>

<main>
  <h1>Hello {name}!</h1>
  <div class="search-block">
    <input type="text" placeholder="Search for gif" bind:value={searchTerm} />
    <button on:click={searchForGif}>Search</button>
  </div>
  <div class="gifs">
    {#if gifs.length > 0}
      <div class="gifs-grid">
        {#each gifs as gif}
          <iframe src={gif.embed_url} title={gif.title} />
        {/each}
      </div>
    {:else}No gifs to show yet{/if}
  </div>
</main>
