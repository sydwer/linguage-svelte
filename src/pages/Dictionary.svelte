<script>
    export let dictionary;
</script>


{#each dictionary as word}
<h2>{word.original} : {word.IPA}, {word.latin}</h2>
{/each}

