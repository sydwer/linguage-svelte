<script>
    export let dictionary;
    export let category
</script>

<style>
    span{
        text-decoration: underline;
        font-weight: bold;
    }
    p{
        padding-left: 1rem;
    }
</style>

<h2>{category}:</h2>
{#each dictionary as word}
<p><span>{word.original}</span>: {word.latin}   (/{word.IPA}/) </p>
{/each}

