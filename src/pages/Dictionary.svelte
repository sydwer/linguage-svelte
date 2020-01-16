<script>
    export let dictionary;
</script>


{#each dictionary as word}
<h2>{word.original} : {word.new}</h2>
{/each}

