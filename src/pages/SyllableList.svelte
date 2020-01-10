<script>
    export let phonemes;
    export let syllableStructure;
    let sounds = undefined
  
    
</script>

<style>
#phoneme-box{
    display: grid;
    grid-template-columns: repeat(9, 1fr)
}
#loading-bar{
    color: #598502;
    display: flex;
    flex-direction: row;
    align-items: center;
}

@keyframes blink {
    0% {
      opacity: .2;
    }
    20% {
      opacity: 1;
    }
    100% {
      opacity: .2;
    }
}

.loading span {
    animation-name: blink;
    animation-duration: 1.4s;
    animation-iteration-count: infinite;
    animation-fill-mode: both;
}

.loading span:nth-child(2) {
    animation-delay: .2s;
}

.loading span:nth-child(3) {
    animation-delay: .4s;
}

</style>

{#if !phonemes}
<h1 id="loading-bar"> Awaiting User Input<p class="loading"><span>.</span><span>.</span><span>.</span></p></h1>
{/if}
<div id="phoneme-box">
    {#if phonemes}
        {#each phonemes as sound}
        <h3>{sound.symbol}</h3>
        {/each}
    {/if}
</div>
    {#if syllableStructure}
    <h3>Your Syllable Structure is {syllableStructure}</h3>
    {/if}
