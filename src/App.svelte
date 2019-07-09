<script>
  import { onMount } from "svelte";
  export let name;
  // @see<https://codepen.io/luizbills/pen/VXKJpO>
  const btnBlue =
    "button-reset white pv2 ph3 bg-blue hover-bg-dark-blue bn br2";
    
  const card = "ba br3 b--black-10 pa2 shadow-4 w-20 tc center mt2 mb2";
  const ulClass =
    "ba b--black-10 list pl0 ml0 center mw5 ba b--light-silver br3";
  const liClass = "ph3 pv2 bb b--light-silver pointer";

  const toggle = () => {
    console.log("toggled");
  };

  const handleSelect = char => {
    console.log(char);
    name = char.name;
  };

  // Fetch data from star wars api
  let characters = [];
  onMount(async () => {
    const apiResponse = await fetch("https://swapi.co/api/people");
    const swapiPeopleJson = await apiResponse.json();
    characters = swapiPeopleJson.results;
  });
</script>

<svelt:head>
  <link
    rel="stylesheet"
    href="https://cdnjs.cloudflare.com/ajax/libs/tachyons/4.11.1/tachyons.css" />

</svelt:head>

<div>
  <div class={card}>
    <h1 class="light-red">
      Hello there
      <br />
       {name}!
    </h1>

    <button class={btnBlue} on:click={toggle}>Ok</button>
  </div>
  <!-- Add logic to highlight selected -->
  <!--  { name, height, birth_year } -->
  <ul class={ulClass}>
    {#each characters as char}
      <li class={liClass} on:click={() => handleSelect(char)}>
        <strong>{char.name}</strong>
        (height: {char.height}cm, birth year: {char.birth_year})
      </li>
    {:else}
      <p>Loading...</p>
    {/each}
  </ul>
</div>
