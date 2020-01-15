<script>
    import { onMount } from 'svelte';
    import ComparisonRow from './ComparisonRow.svelte'
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
</style>


{#if native_language}
<div id="main">
    <div id="comparison-info-header" class = "comparison-row">
        <span></span>
        <h1>{comparison.native_language.name}:</h1>
        <h1> vs.</h1>
        <h1>{comparison.target_language.name}:</h1>
    </div>
    <ComparisonRow rowName= "General Language Family:" nativeLanguageInfo={native_language.language_family.general_family}
        targetLanguageInfo={target_language.language_family.general_family} />

    <ComparisonRow rowName=" Specific Language Family:" nativeLanguageInfo={native_language.language_family.specific_family}
        targetLanguageInfo= {target_language.language_family.specific_family}/>

    <ComparisonRow rowName="Grammar/Morphology" nativeLanguageInfo={native_language.morphology.name} 
        targetLanguageInfo={target_language.morphology.name}/>

    <ComparisonRow rowName= "Number of Noun Classes:" nativeLanguageInfo={native_language.noun_classes} 
        targetLanguageInfo={target_language.noun_classes}/>

    <ComparisonRow rowName="Number of Sounds Used:" nativeLanguageInfo={native_language.phonemes.length} 
        targetLanguageInfo={target_language.phonemes.length}/>
</div>
<!-- TRANSFER THESE ROWS INTO A COMPONENT WHEN YOU HAVE TIME -->
{/if}