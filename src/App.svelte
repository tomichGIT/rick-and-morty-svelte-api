<script>
  import Character from "./lib/Character.svelte";
  import Location from "./lib/Location.svelte";
  import Episode from "./lib/Episode.svelte";

  //defaults
  let characters = [];
  let episodes = [];
  let locations = [];
  let section; // characters, episodes, locations

  let page, count, pages; // cantidad y páginas

  async function loadCharacters() {
    const response = await fetch(
      "https://rickandmortyapi.com/api/character?page=" + page
    );
    const data = await response.json();
    characters = data.results;
    count= data.info.count;
    pages = data.info.pages;
  }
  async function loadEpisodes() {
    const response = await fetch(
      "https://rickandmortyapi.com/api/episode?page=" + page
    );
    const data = await response.json();
    episodes = data.results;
    count= data.info.count;
    pages = data.info.pages;
  }
  async function loadLocations() {
    const response = await fetch(
      "https://rickandmortyapi.com/api/location?page=" + page
    );
    const data = await response.json();
    locations = data.results;
    count= data.info.count;
    pages = data.info.pages;
  }

  function nextPage() {
    page++;
    switch(section){
      case "characters":loadCharacters(); break;
      case "locations":loadLocations(); break;
      case "episodes":loadEpisodes(); break;
    }
  }

  function previousPage() {
    page--;
    switch(section){
      case "characters":loadCharacters(); break;
      case "locations":loadLocations(); break;
      case "episodes":loadEpisodes(); break;
    }
  }

  /**
  * @param {string} sec
  */
  function handleSection(sec){
    page=0;
    section=sec;
    nextPage();
  }

  handleSection("characters");
</script>

<main class="container">
  <h1 class="title">Rick And Morty Svelte ({section})</h1>

  <div class="btns">
    <button class="btn" on:click={()=>handleSection("characters")}>Personajes </button>
    <button class="btn" on:click={()=>handleSection("episodes")}>Episodios </button>
    <button class="btn" on:click={()=>handleSection("locations")}>Lugares </button>
  </div>


  <div class="btns">
    <button on:click={previousPage} disabled={page === 1}>Previous</button>
    <div>Cant: {count} / Página: {page}/{pages}</div>
    <button class="btn" on:click={nextPage} disabled={page === pages}>Next</button>
  </div>

  <div class="grid">
    {#if section=="characters"}
      {#each characters as character}
        <Character {character} />
      {/each}
    {:else if section=="locations"}
      {#each locations as location}
        <Location {location} />
      {/each}
    {:else if section=="episodes"}
      {#each episodes as episode}
        <Episode {episode} />
      {/each}
    {/if}
  </div>
</main>
