<script>
import { onMount } from 'svelte';
    export let comparison;
    let languages = undefined;
    let native_language = undefined;
    let target_language = undefined;
    let newPhonemes = [];

    onMount(async function() {
        const response = await fetch("http://127.0.0.1:3000/languages");
        const json = await response.json();
        languages = json;
        native_language = languages.find(obj=>obj.name===comparison.native_language.name)
        target_language = languages.find(obj=>obj.name===comparison.target_language.name)
        // findNewPhonemes(native_language, target_language)
        console.log(native_language)
    });

    // function findNewPhonemes(native_language, target_language){
    //     var i;
    //     for(i = 0; i < target_language.phonemes.length; i++){
    //         if (native_language.phonemes.includes(target_language.phonemes[i])){
    //             console.log("includes it")
    //         }else{
    //             console.log("excludes")
    //         }
    //     }
    // }
</script>

<style>
#main{
    width: 100%;
    
}
.comparison-row{
    display:grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
}

h1{
    display: flex;
    justify-content: center;
    text-decoration: underline;
}
h3{
    display: flex;
    justify-content: center;
    align-items: center;
}
h2{
    display: flex;
    justify-content: center;
    align-items: center;
    padding-right: 10px;
}

</style>


{#if native_language}
<div id="main">
    <div id="comparison-info-header" class = "comparison-row">
        <span></span>
        <h1>{comparison.native_language.name}:</h1>
        <h1> vs.</h1>
        <h1>{comparison.target_language.name}:</h1>
    </div>
      <div class = "comparison-row">
        <h2>Language Family:</h2>
        <h3>{native_language.language_family.general_family},{native_language.language_family.specific_family}</h3>
        <h3> - </h3>
        <h3>{target_language.language_family.general_family},{target_language.language_family.specific_family}</h3>
    </div>
    <div class = "comparison-row">
        <h2>Grammar/Morphology:</h2>
        <h3>{native_language.morphology.name}</h3>
        <h3> - </h3>
        <h3>{target_language.morphology.name}</h3>
    </div>
    <div class = "comparison-row">
        <h2>Number of Noun Classes:</h2>
        <h3>{native_language.noun_classes}</h3>
        <h3> - </h3>
        <h3>{target_language.noun_classes}</h3>
    </div>
    <div class = "comparison-row">
        <h2>Number of Sounds Used:</h2>
        <h3>{native_language.phonemes.length}</h3>
        <h3> - </h3>
        <h3>{target_language.phonemes.length}</h3>
    </div>
</div>
<!-- TRANSFER THESE ROWS INTO A COMPONENT WHEN YOU HAVE TIME -->
{/if}