<script>
import { onMount } from 'svelte';
    export let comparison;
    let languages = undefined;
    let native_language = undefined;
    let target_language = undefined;

    onMount(async function() {
        const response = await fetch("http://127.0.0.1:3000/languages");
        const json = await response.json();
        languages = json;
        native_language = languages.find(obj=>obj.name===comparison.native_language.name)
        target_language = languages.find(obj=>obj.name===comparison.target_language.name)
        console.log(native_language)
    });

</script>

<style>
#main{
    width: 75%;
}
#comparison-info-header{
    display:grid;
    grid-template-columns: 1fr 1fr 1fr;
}
h1{
    display: flex;
    justify-content: center;
}
</style>

<div id="main">
<div id="comparison-info-header">
    <h1>{comparison.native_language.name}:</h1>
    <h1> vs.</h1>
    <h1>{comparison.target_language.name}:</h1>
</div>
    <!-- <div class = "comparison-row">
    <h3>Grammar:{comparison.native_language.morphology.name}</h3>
    <h3> - </h3>
    <h3>{comparison.target_language.morphology.name}</h3>
    </div> -->
</div>