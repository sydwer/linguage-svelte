<script>
    import ConjugationRow from './ConjugationRow.svelte'
    export let allInfo;
    export let columns;
    let filteredInfo = allInfo

    if(columns === "-1"){
        const noFutureTense = allInfo.filter(function(info) {
               return info.original !== "Future";
            })
            filteredInfo = noFutureTense
        const nonPast = filteredInfo.find(obj => obj.original === 'Present')
        nonPast.original = "Non-Past"
    }
</script>

<style>
    #columns2{
        display: grid;
        grid-template-columns: 1fr 1fr;
        grid-column-gap: 1rem;
    }
    div{
        width: 75%;
    }
</style>
<!-- <h2>{grammarOrigin.name}</h2> -->
{#if columns === "2"}
<div id="columns2">
    {#each filteredInfo as info}
        <ConjugationRow info={info.original} generatedInfo={info.latin}/>
    {/each}
</div>
{:else}
<div id="columns1">
    {#each filteredInfo as info}
        <ConjugationRow info={info.original} generatedInfo={info.latin}/>
    {/each}
</div>
{/if}