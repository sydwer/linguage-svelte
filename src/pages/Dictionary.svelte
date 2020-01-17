<script>
    export let dictionary;
</script>


{#each dictionary as word}
<h2>{word.original} : {word.latin} IPA: {word.IPA} </h2>
{/each}

