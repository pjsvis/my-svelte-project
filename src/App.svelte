<script>
  import { onMount } from "svelte";
  import {
    btnBlue,
    card,
    ulClass,
    liClass,
    liSelectedClass
  } from "./styles/Styles.svelte";
  export let name;

  const toggle = () => {
    console.log("toggled");
  };

  let selectedChar = "";
  const handleSelect = char => {
    console.log(char);
    name = char.name;
    selectedChar = char.name;
    console.log(selectedChar);
  };

  // Fetch data from star wars api
  let characters = [];

  onMount(async () => {
    const apiResponse = await fetch("https://swapi.co/api/people");
    const swapiPeopleJson = await apiResponse.json();
    characters = swapiPeopleJson.results;
    handleSelect(characters[0]);
  });
</script>

<svelt:head>
  <link
    rel="stylesheet"
    href="https://cdnjs.cloudflare.com/ajax/libs/tachyons/4.11.1/tachyons.css" />

</svelt:head>

<div class="flex flex-order-1 w-50 center">
  <ul class={ulClass}>
    {#each characters as char}
      <li
        class={char.name === selectedChar ? liSelectedClass : liClass}
        on:click={() => handleSelect(char)}>
        <strong>{char.name}</strong>
        (height: {char.height}cm, birth year: {char.birth_year})
      </li>
    {:else}
      <p class="w-100 pa3">Loading...</p>
    {/each}
  </ul>
  {#if name.length > 0}
    <div class={card}>
      <h1 class="light-red">
        Hello there
        <br />
         {name}!
      </h1>

      <button class={btnBlue} on:click={toggle}>Ok</button>
    </div>
  {/if}

</div>
