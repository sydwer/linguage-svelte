<script>
    export let dictionary;
    export let category;

  

  
</script>

<style>

    span{
        text-decoration: underline;
        font-weight: bold;
    }
    h2{
        padding-left: 1rem;
    }
    p{
        padding-left: 2rem;
    }
</style>

<h2>{category}:</h2>


{#each dictionary as word}
<p><span>{word.original}</span>: {word.latin}   (/{word.IPA}/) </p>
{/each}


