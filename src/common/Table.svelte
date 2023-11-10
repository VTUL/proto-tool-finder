<script>
  import {
    DataTable,
    Toolbar,
    ToolbarContent,
    ToolbarSearch,
  } from "carbon-components-svelte";
  import Map from "./Map.svelte";
  import words from "lodash.words";
  let activeShelf;
  export let data = [];
  export let search = "";

  function searchTable(search, fullData) {
    console.log(fullData);
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
  <DataTable
    title="Tools Available"
    description="Search to find a tool you're looking for and click on it to see its location in the cabinets."
    headers={[
      { key: "Item", value: "Tool Name" },
      { key: "Quantity", value: "Quantity" },
      { key: "Category", value: "Category" },
    ]}
    rows={searchTable(search, data)}
    on:click:row={(event) => {
      if (activeShelf) {
        activeShelf.style.visibility = "hidden";
      }
      activeShelf = document.getElementById(event.detail["Location"]);
      activeShelf.style.visibility = "visible";
    }}
  >
    <Toolbar>
      <ToolbarContent>
        <ToolbarSearch persistent bind:value={search} />
      </ToolbarContent>
    </Toolbar>
  </DataTable>
</main>

<style>
</style>
