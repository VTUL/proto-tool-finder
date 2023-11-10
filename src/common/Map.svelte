<script>
    import map from "./example.svg";
    import {Button} from 'carbon-components-svelte';
    import {table} from './stores';
    import { onMount } from "svelte";

    onMount(async () => {
        const baskets = document.getElementById("baskets").getElementsByTagName("g"); 
        for(let i = 0; i<baskets.length; i++) {
            baskets[i].style.visibility = "hidden";
        };
    });

</script>

<div id="header">
    <Button on:click={() => {
        window.location.reload();
    }}>Start Over</Button>
    <Button on:click={() => {
        table.set(!$table);
    }}>Switch to {$table ? "Catalog View" : "Table View"}</Button>
</div>
<div class="map-container">
    {@html map}
</div>

<style>

</style>