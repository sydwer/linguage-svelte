<script>
    export let phonemes;
    export let syllableStructure;
    
function playAudio(url) {
    var a = new Audio(url);
    a.play();
}

</script>

<style>
#sound-box{
    display: flex;
    flex-direction: column;
}
#sound-box>h2{
    text-decoration: underline;
}

h2>span{
   text-decoration: underline; 
}
#phoneme-box>h3:hover{
    text-decoration: underline;
    color: #749e02;
    transform: scale(1.02)
}
#phoneme-box{
    width: 66%;
    display: grid;
    grid-template-columns: repeat(9, 1fr);
    grid-gap: 25px;
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
<div id="sound-box">
    {#if phonemes}
    <h2>Sound Inventory:</h2>
    <h4>(Click on a symbol to hear what it sounds like)</h4>
    <!-- <h7>*Dipthongs have unconvential sound file, that utilizes a sentance encompassing them all, rather than the single one clicked on</h7> -->
    <div id="phoneme-box">
        {#each phonemes as sound}
        <h3 on:click={()=>{playAudio(sound.sound_url)}}>{sound.symbol}</h3>
        {/each}
    </div>
    {/if}
</div>
    {#if syllableStructure}
    <h2><span>Syllable Structure:</span> "{syllableStructure.join("")}"</h2>
    {/if}
