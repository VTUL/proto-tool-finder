<script>
    import Map from "./Map.svelte";
    import words from "lodash.words";
    import { Search } from "carbon-components-svelte";
    import placeholder from "./tool-generic.svg";
    let activeShelf;
    let activeItem;
    export let data = [];
    export let search = "";
  
    function searchCatalog(search, fullData) {
      if (search === "" || search === null) {
        return [...fullData];
      } else {
        let temp = [...fullData];
        temp = temp.filter((item) => {
          let results = words(search.toLowerCase()).map((word) => {
            let test = false;
            let searchFields = ["Item", "Category"];
            searchFields.forEach((field) => {
              if (item[[field]].toLowerCase().includes(word)) test = true;
            });
            return test;
          });
          return results.every((value) => value) ? true : false;
        });
        return [...temp];
      }
    }
  </script>
  
  <main>
    <Map />
    <div id="search-container">      
      <Search bind:value={search} />
    </div>
    <div id="catalog-container">
        {#each searchCatalog(search, data) as tool}
            <div class="catalog-item" id={tool.id} on:click={(event) => {
              if (activeShelf) {
                activeShelf.style.visibility = "hidden";
              }
              if (activeItem) {
                activeItem.style.borderColor = "#e5e1e6";
              }
              activeShelf = document.getElementById(tool["Location"]);
              activeShelf.style.visibility = "visible";
              activeItem = document.getElementById(tool.id);
              activeItem.style.borderColor = '#861f41';
            }}>
                {#if tool.Photo}
                  <img class="tool-image" alt="Image of a {tool['Item']}" src={tool.PhotoLink} />
                {:else}
                  {@html placeholder}
                {/if}
                <p class="tool-name">{tool['Item']}</p>
                <p class="quantity">Quantity: {tool['Quantity']}</p>
                <p class="location">Location: {tool['Location']}</p>
            </div>
        {/each}
    </div>
  </main>
  
  <style>
  </style>