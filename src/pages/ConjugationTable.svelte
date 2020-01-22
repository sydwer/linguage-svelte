<script>
    import ConjugationRow from './ConjugationRow.svelte'
    export let pronouns;
</script>

<style>
    #table{
        display: grid;
        grid-template-columns: 1fr 1fr;
    }
</style>
<!-- <h2>{grammarOrigin.name}</h2> -->
<div id="table">
    {#each pronouns as pronoun}
        <ConjugationRow pronoun={pronoun.original} generatedPronoun={pronoun.latin}/>
    {/each}
    
</div>