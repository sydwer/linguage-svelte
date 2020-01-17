<script>
// import {onMount } from 'svelte'
import Dictionary from './Dictionary.svelte'
export let syllableBank;
export let mary;
export let john;


    const genericDictionary = [{original: "Cat", new: undefined}, {original: "Hello", new: undefined},{original: "Book", new:undefined},{original: "Tree", new: undefined},
        {original: "Dinner", new: undefined}, {original: "Apple", new: undefined}, {original: "Fish", new: undefined},{ original: "House", new: undefined},
        {original: "River", new: undefined}, {original: "Bear", new: undefined}, {original: "Hunger", new: undefined}, {original: "Say", new: undefined},
        {original: "Give", new: undefined}, {original: "Copula", new: undefined}, {original: "Die", new: undefined}, {original: "Eat", new: undefined},
        {original: "Have", new: undefined}, {original: "Want", new: undefined}, {original: "Big", new: undefined}, {original: "Hungry", new: undefined},
        {original: "Cute", new: undefined}, {original: "Fast", new: undefined}, {original: "Ten", new: undefined},];

    const pronounDictionary = [{original: "I", new: undefined},{original:"You", new: undefined},{original:"He", new: undefined},{original:"She", new: undefined},
    {original:"It", new: undefined},{original:"We", new: undefined},{original:"You (Plural)", new: undefined},{original:"They", new: undefined},]

    // ^^^Sort alphabetically and by part of speech^^^// 
    if(syllableBank){
        makeDictionary(genericDictionary);
        makeDictionary(pronounDictionary)
    }

    function makeBoundMorpheme(syllables){
        const morpheme = syllables[Math.floor(Math.random() * syllables.length)]
        return morpheme
    }

    function makeFreeMorpheme(syllables){
        //want 2-4 syllables so 1-3, and then add one?
        const randomWordSyllables =[]
        let syllableAmount = undefined;
        const randomNumber = Math.floor(Math.random() * 3)
        if (randomNumber < 2){
            syllableAmount = 2;
        }else{
            syllableAmount = randomNumber
        }
        // console.log(syllableAmount)
        var i;
        for(i = 0; i < syllableAmount; i ++){
            randomWordSyllables.push(syllables[Math.floor(Math.random() * syllables.length)])
        }
        const joinedRandomWord = randomWordSyllables.join("")
        return joinedRandomWord
    }


    function makeDictionary(dictionary){
        var i;
        for (i = 0; i < dictionary.length; i++){
            dictionary[i].new = makeFreeMorpheme(syllableBank)
        }
    }

</script>

<style>
    
</style>

<h1>Agglutinative Grammar Component Test:</h1>
<h2>{mary} {john} </h2>


<Dictionary dictionary={genericDictionary}/>
<Dictionary dictionary={pronounDictionary}/>


<!-- <h4>{dictionary}</h4> -->