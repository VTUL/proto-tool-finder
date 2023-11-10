<script>
  import { Greeting, Table, Footer, Catalog } from "./common";
  import { onMount } from "svelte";
  import { table, greeting } from './common/stores';
  import Papa from "papaparse";
  import { v4 as uuidv4 } from "uuid";
  let data = [];
  let search = "";

  onMount(async () => {
    Papa.parse(
      "url to your spreadsheet needed",
      {
        download: true,
        header: true,
        complete: function (results) {
          data = results.data.map((value) => {
            return { id: uuidv4(), ...value };
          });
          // data = results.data
        //   console.log(data);
        },
        error: function (err) {
          console.log(err);
        },
      }
    );
  });
</script>

{#if $greeting}
  <Greeting bind:search />
{:else if !$table}
  <Catalog bind:search {data} />
{:else}
  <Table bind:search {data} />
{/if}
<Footer />

<style>
</style>
