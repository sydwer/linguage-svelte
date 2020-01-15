<script>
    import { onMount } from 'svelte'

    let languages = undefined;
    let selectedLanguage = undefined;

    onMount(async function() {
        const response = await fetch("http://127.0.0.1:3000/languages");
        const json = await response.json();
        languages = json;
    });

    function pickLanguage(language){
        console.log(language.name)
    }
</script>


<style>
    h1{
        padding-left: 1rem;
        text-decoration: underline
    }
    h3{
        padding-left: 2rem;
    }
    #main{
        display: flex;
        justify-content: center
    }
    #card-grid{
        width: 90%;
        display: grid;
        grid-template-columns: repeat(5,1fr);
        grid-gap: 15px;

    }
    .card{
        display: flex;
        flex-direction: column;
        align-items: center;
        border: 2px solid black;
        border-radius: 5px;
        padding: 1rem;
    }
    .card:hover{
        box-shadow: 5px 5px 25px grey;
        transform: scale(1.02);
        color: #749e02;
    }
    .card>img{
        /* width: 5rem; */
        height: 6rem;
    }

   
</style>


<h1>Explore:</h1>
{#if !selectedLanguage}
<h3>Pick a Language to Learn More About It</h3>
{/if}
<div id= "main">
{#if languages}
    <div id="card-grid">
        {#each languages as language}
        <div class = "card" on:click={()=>{ pickLanguage(language)}}>
            <img src="https://www.countryflags.io/{language.flag}/shiny/64.png" alt= "flag">
            <h2>{language.name}</h2>
        </div>
        {/each}
    </div>
{/if}
</div>