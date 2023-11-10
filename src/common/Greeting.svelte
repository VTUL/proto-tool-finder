<script>
  import {greeting} from './stores';
  import {Search} from 'carbon-components-svelte';
  let options = [
    "Woodworking",
    "Molding Clay",
    "Electronics",
    "3D Printing",
    "Disassembling/Assembling Something",
    "Getting Measurements",
    "Finishing/Cleaning an Object",
  ];

  export let search;

  function handleClick(option) {
    greeting.set(false);
    if (option) {
      search = option;
    }
  }
</script>

<main id="greeting-main">
  <h1 id="greeting">What kind of project are you working on today?</h1>
  <div id="options-container">
    {#each options as option}
      <button
        class="option"
        on:click={() => {
          handleClick(option);
        }}>{option}</button
      >
    {/each}
  </div>
  <h2>Or you can</h2>
  <div id="search-container">      
    <Search bind:value={search} />
  </div>
  <div id="show-search">
    <button
      id="show-search-button"
      on:click={() => {
        handleClick(false);
      }}>Search the Tools</button
    >
  </div>
</main>

<style>
  h1#greeting, h2 {
    font-size: 4rem;
    color: #861f41;
    padding: 3rem;
    text-align: center;
    font-weight: 300;
  }
  button.option {
    font-size: 2rem;
    color: white;
    background-color: #861f41;
    border: 2px solid transparent;
    padding: 1rem 3rem;
    text-transform: uppercase;
    cursor: pointer;
    border-color: #a52650;
    box-shadow: 0 0 10px rgb(102 102 102 / 70%);
  }
  div#options-container {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
    margin-bottom: 3rem;
    align-items: center;
    gap: 2rem;
  }
  button#show-search-button {
    color: white;
    background-color: #508590;
    border: 2px solid transparent;
    font-size: 2.5rem;
    padding: 2rem 3rem;
    text-transform: uppercase;
    cursor: pointer;
    border-color: #6aafbb;
    box-shadow: 0 0 10px rgb(102 102 102 / 70%);
  }
  div#show-search {
    display: flex;
    width: 100%;
    justify-content: center;
  }
</style>
