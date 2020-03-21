<script>
    import ConjugationRow from './ConjugationRow.svelte'
    export let allInfo;
    export let columns;
    

 
</script>

<style>
    #columns2{
        display: grid;
        grid-template-columns: 1fr 1fr;
        grid-column-gap: 1rem;
        width: 100%;
    }
    #columns1{
        width: 75%;
    }
</style>
<!-- <h2>{grammarOrigin.name}</h2> -->
{#if columns === "2"}
<div id="columns2">
    {#each allInfo as info}
        <ConjugationRow info={info.original} generatedInfo={info.latin}/>
    {/each}
</div>
{:else}
<div id="columns1">
    {#each allInfo as info}
        <ConjugationRow info={info.original} generatedInfo={info.latin}/>
    {/each}
</div>
{/if}