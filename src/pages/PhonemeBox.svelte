<script>
    export let phonemes;
    
function playAudio(url) {
    var a = new Audio(url);
    a.play();
}

</script>

<style>
#sound-box{
    display: flex;
    flex-direction: column;
    align-items: center;
}
#sound-box>h2{
    text-decoration: underline;
}

h4{
    margin-top: 0;
}
#phoneme-box>h3{
    padding: 15px;
}
#phoneme-box>h3:hover{
    text-decoration: underline;
    color: #749e02;
    transform: scale(1.02)
}
#phoneme-box{
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    border: 3px solid black;
    border-radius: 7px;
}
</style>


<div id="sound-box">
    {#if phonemes}
    <h2>Sound Inventory:</h2>
    <h4>(Click on a symbol to hear what it sounds like)</h4>
    <div id="phoneme-box">
        {#each phonemes as sound}
        <h3 on:click={()=>{playAudio(sound.sound_url)}}>{sound.symbol}</h3>
        {/each}
    </div>
    {/if}
</div>

