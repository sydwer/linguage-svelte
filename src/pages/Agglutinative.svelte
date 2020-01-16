<script>
// import {onMount } from 'svelte'
import Dictionary from './Dictionary.svelte'
export let syllableBank;
export let mary;
export let john;


    const genericDictionary = [{original: "cat", new: undefined}, {original: "hello", new: undefined},{original: "book", new:undefined},{original: "tree", new: undefined},
        {original: "dinner", new: undefined}, {original: "apple", new: undefined}, {original: "fish", new: undefined},{ original: "house", new: undefined},
        {original: "river", new: undefined}, {original: "bear", new: undefined}, {original: "hunger", new: undefined}, {original: "say", new: undefined},
        {original: "give", new: undefined}, {original: "copula", new: undefined}, {original: "die", new: undefined}, {original: "eat", new: undefined},
        {original: "have", new: undefined}, {original: "want", new: undefined}, {original: "big", new: undefined}, {original: "hungry", new: undefined},
        {original: "cute", new: undefined}, {original: "fast", new: undefined}, {original: "ten", new: undefined},];

    const pronounDictionary = [{original: "I", new: undefined},{original:"you", new: undefined},{original:"he", new: undefined},{original:"she", new: undefined},
    {original:"it", new: undefined},{original:"we", new: undefined},{original:"you all", new: undefined},{original:"they", new: undefined},]


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
        const syllableAmount = (Math.floor(Math.random() * 2) + 1)
        const randomWordSyllables =[]
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