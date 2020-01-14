<script>
    import { onMount } from "svelte";
    import ComparisonBox from './ComparisonBox.svelte'

    let comparisons = undefined;
    let filteredComparisons = undefined;
    let activeComparison = undefined;

    onMount(async function() {
        const response = await fetch("http://127.0.0.1:3000/comparisons");
        const json = await response.json();
        comparisons = json;
    });

    function sayHi(comparison){
        console.log(comparison.native_language.hello)
        activeComparison = comparison
    }
</script>
<style>
    #main{
        display: flex;
        flex-direction: row;
    }
    #comparison-list{
        display: flex;
        flex-direction: column;
        align-items: center;
        border: 2px solid black;
        /* width: 25%; */
        height: 25rem;
        overflow: scroll;
    }
    #one-comparison{
        display: grid;
        grid-template-columns: repeat(3,1fr);
    }
    h3{
        display: flex;
        align-items: center;
        justify-content: center;
    }

</style>
<!-- ■ -->
<h1>Comparisons</h1>
<div id = "main">
{#if comparisons}
<div id="comparison-list">
        {#each comparisons as comparison}
        <div id="one-comparison" on:click={()=>{sayHi(comparison)}}>
        <h3> {comparison.native_language.name} </h3><h3>-></h3><h3>{comparison.target_language.name}</h3>
        </div>
        {/each}
    </div>
{/if}
{#if activeComparison}
<ComparisonBox comparison={activeComparison}/>
{/if}
</div>
