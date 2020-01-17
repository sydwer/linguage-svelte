<script>
    import { onMount } from 'svelte';
    import ComparisonBox from './ComparisonBox.svelte';
    import Loading from '../layout/Loading.svelte';

    let comparisons = undefined;
    let languages = undefined;
    let activeComparison = undefined;
    // let native_language = undefined;
    // let target_language = undefined;

    onMount(async function() {
        const response = await fetch("http://127.0.0.1:3000/comparisons");
        const json = await response.json();
        comparisons = json;
        // const response2 = await fetch("http://127.0.0.1:3000/languages");
        // const json2 = await response2.json();
        // languages = json2;
        // native_language = languages.find(obj=>obj.name===comparison.native_language.name)
        // target_language = languages.find(obj=>obj.name===comparison.target_language.name)
    });


    function pickComparison(comparison){
        // console.log(comparison.native_language.hello)
        activeComparison = comparison
        // native_language = languages.find(obj=>obj.name===comparison.native_language.name)
        // target_language = languages.find(obj=>obj.name===comparison.target_language.name)
        // console.log(activeComparison.target_language)
    }
    function resetPage(){
        activeComparison = undefined;
    }
</script>
<style>
@import url('https://fonts.googleapis.com/css?family=Solway|Sulphur+Point&display=swap');
    /* *{font-family: 'Solway', serif;} */
    #main{
        display: flex;
        flex-direction: row;
    }
    h1{
        padding-left: 1rem;
        text-decoration: underline;
    }
    h2{
        padding-left: 2rem;
        margin: 0;
    }
    h5{
        display: flex;
        justify-content: center;
        padding-left:3rem;
        margin: 0;
        margin-top: 5px;
        margin-bottom: 5px;
    }
    h4{
        margin: 0;
        margin-top: 5px;
    }
     #comparison-box{
        padding-left: 3rem;
        display: flex;
        flex-direction: row;
        height: 25rem;
    }
    img{
        width: 2rem;
        border: 2px solid black;
        border-right: 0;
        border-radius: 5px 0px 0px 5px;
    }
    #comparison-list{
        border-radius: 0px 5px 5px 0px;
        display: flex;
        flex-direction: column;
        align-items: center;
        border: 2px solid black;
        overflow-y: scroll;
    }
    #one-comparison{
        display: grid;
        grid-template-columns: repeat(3,1fr);
        padding-left: 10px;
        padding-right: 10px;
    }
    #one-comparison:hover{
        text-decoration: underline;
        color: #749e02;
        transform: scale(1.02)
    }
    h3{
        display: flex;
        align-items: center;
        justify-content: center;
    }
    #key-points-box{
        font-family: 'Solway', serif;
        width: 75%;
        display: flex;
        flex-direction: column;
        align-items: center;
        padding-bottom: 30px;
    }
  
    p{
        font-size: larger
    }
    #comparison-header{
        width: 33%;
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    button{
        margin-top: 1rem;
        margin-left: 1rem;
        font-weight: bold;
        position: relative;
        width: 18%;
        height: 2.3rem;
        background-color: #86ba3247;
        border-radius: 15px;
        border: 1px solid #293801;
        font-size: 1rem;
    }
    button:hover{
        text-decoration: none;
        border-radius: 15px;
        /* width: 90%; */
        background-color: #749e02;
        color: white;
    }
    #loading-container{
        position: absolute;
        top: 50%;
        left: 50%;
    }


</style>
<!-- ■ -->

{#if !comparisons}
    <div id="loading-container">
        <Loading message="Loading"/>
    </div>
{/if}

{#if activeComparison}
<button on:click={()=>{ resetPage()}}>⬅ Return to Comparisons</button>
<ComparisonBox comparison={activeComparison}/>
{/if}

{#if comparisons && !activeComparison}
<h1>Compare:</h1>
<div id="comparison-header">
    <h2>Languages, Easiest to Hardest to Learn</h2>
    <h4>*Click on a comparison to see more information*</h4>
</div>
{/if}

{#if comparisons && !activeComparison}
<div id = "main">
{#if comparisons}
    <div id = "comparison-selection">
    <h5> Starting Language --> New Language </h5>
        <div id="comparison-box">
        <img id="gradient" src="./media/gradient.png" alt="gradient">
        <div id="comparison-list">
            {#each comparisons as comparison}
            <div id="one-comparison" on:click={()=>{pickComparison(comparison)}}>
            <h3> {comparison.native_language.name} </h3><h3>-></h3><h3>{comparison.target_language.name}</h3>
            </div>
            {/each}
        </div>
        </div>
        </div>
<!-- {/if} -->
<!-- {#if  comparisons && !activeComparison} -->
<div id="key-points-box">
           <h2>What Makes a Language "Easier to Learn"?</h2>
           <p>The more similar languages are, i.e the less "new" stuff you have<br/> 
            to know, the easier they are to learn. With this in mind, lɪŋˈ-guage has<br/> 
            developed a system that stores information on languages including where<br/> 
            they're from, what their grammar and writing looks like - and even how<br/> 
            many sounds they have. Then lɪŋˈ-guage pushes all of this into an equation<br/> 
            that compares these traits, and gets out a number that represents how<br/> 
            different they are from eachother.<br/>       
            <br/>
            This number is what lɪŋˈ-guage uses to sort the language comparisons.<br/> 
            It presents them to you in order of similarity between the pairs. So, the <br/>
            easiest language transitions are shown first, and the hardest language<br/>
            learning pairs are at the end.
            <br/>
            <br/>
            Click on a comparison within the list to see a brief summary of the <br/>
            similarities and differences between the two languages.
           </p>
        </div>
    <!-- {/if} -->
{/if}
</div>
{/if}
