<script>
// import {onMount } from 'svelte'
import Dictionary from './Dictionary.svelte'
import ConjugationTable from './ConjugationTable.svelte'
export let syllableBank;
export let mary;
export let john;
export let grammarOrigin;

    const names = [{IPA: mary, latin: "Mary"},{IPA: john, latin: "John"}];

    const nouns = [{original: "Apple", IPA: undefined, latin: undefined},{original: "Bear", IPA: undefined, latin: undefined},
        {original: "Book", IPA: undefined, latin: undefined}, {original: "Cat", IPA: undefined, latin: undefined}, 
        {original: "Dinner", IPA: undefined, latin: undefined}, {original: "Fish", IPA: undefined, latin: undefined},
        {original: "Hello", IPA: undefined, latin: undefined}, {original: "House", IPA: undefined, latin: undefined},
        {original: "Hunger", IPA: undefined, latin: undefined}, {original: "River", IPA: undefined, latin: undefined},
        {original: "Ten", IPA: undefined, latin: undefined}, {original: "Time", IPA: undefined, latin: undefined},
        {original: "Tree", IPA: undefined, latin: undefined},
        ];

    const verbs = [{original: "Eat", IPA: undefined, latin: undefined}, {original: "Enjoy", IPA: undefined, latin: undefined},
        {original: "Die", IPA: undefined, latin: undefined}, {original: "Give", IPA: undefined, latin: undefined}, 
        {original: "Have", IPA: undefined, latin: undefined}, {original: "Say", IPA: undefined, latin: undefined}, 
        {original: "To Be", IPA: undefined, latin: undefined}, {original: "Want", IPA: undefined, latin: undefined},
        ];

    const adjectives = [{original: "Big", IPA: undefined, latin: undefined}, 
        {original: "Cute", IPA: undefined, latin: undefined}, {original: "Fast", IPA: undefined, latin: undefined}, 
        {original: "Hungry", IPA: undefined, latin: undefined},
        ];

    const pronouns = [{original: "I", IPA: undefined, latin: undefined},{original:"We", IPA: undefined, latin: undefined},
        {original:"You", IPA: undefined, latin: undefined},{original:"You all", IPA: undefined, latin: undefined},
        {original:"He", IPA: undefined, latin: undefined},{original:"She", IPA: undefined, latin: undefined},
        {original:"It", IPA: undefined, latin: undefined},{original:"They", IPA: undefined, latin: undefined},
        ];

    const tenses =[{original: "Present", IPA: undefined, latin: undefined},{original: "Past", IPA: undefined, latin: undefined},
        {original: "Future", IPA: undefined, latin: undefined}, {original: "Imperfect", IPA: undefined, latin: undefined},
        {original: "Conditional", IPA: undefined, latin: undefined},
        ];
    
    const affixes =[{original: "Topic", IPA: undefined, latin: undefined},{original:"Subject", IPA: undefined, latin: undefined},
        {original: "Object", IPA: undefined, latin: undefined},{original: "Also/Too", IPA: undefined, latin: undefined},
        {original: "To/From/By", IPA: undefined, latin: undefined}, {original: "Location/At", IPA: undefined, latin: undefined},
        {original: "And", IPA: undefined, latin: undefined},{original: "Possesive", IPA: undefined, latin: undefined},
        {original: "Question Marker", IPA: undefined, latin: undefined},]

    // ^^^Sort alphabetically and by part of speech^^^// 
    if(syllableBank){
        makeDictionary(nouns);
        makeDictionary(verbs);
        makeDictionary(adjectives);
        makeDictionary(pronouns);
        makeDictionary(tenses);
        makeDictionary(affixes);
    }

    function makeBoundMorpheme(syllables){
        const morpheme = syllables[Math.floor(Math.random() * syllables.length)]
        return morpheme
    }

    function makeFreeMorpheme(syllables){
        //want 2-4 syllables so 1-3, and then add one?
        const randomSyllablesIPA = []
        const randomSyllablesLatin = []
        let syllableAmount = undefined;
        const randomNumber = Math.floor(Math.random() * 10)
        if (randomNumber < 2){
            syllableAmount = 1;
        }else if(randomNumber < 9){
            syllableAmount = 2
        }else{
            syllableAmount = 3
        }
        // console.log(syllableAmount)
        var i;
        for(i = 0; i < syllableAmount; i ++){
            const randomSyllable = syllables[Math.floor(Math.random() * syllables.length)]
            randomSyllablesIPA.push(randomSyllable.IPA)
            randomSyllablesLatin.push(randomSyllable.latin)
        }
        const joinedRandomIPA = randomSyllablesIPA.join("")
        const joinedRandomLatin = randomSyllablesLatin.join("")
        const newWord = {IPA: joinedRandomIPA, latin: joinedRandomLatin}
        return newWord
    }


    function makeDictionary(dictionary){
        let newWord = undefined;
        var i;
        for (i = 0; i < dictionary.length; i++){
            if (dictionary === tenses){
                newWord = makeBoundMorpheme(syllableBank)
            }else{
                newWord = makeFreeMorpheme(syllableBank)
            }
            dictionary[i].IPA = newWord.IPA
            dictionary[i].latin = newWord.latin
        }
        console.log(tenses)
    }

</script>

<style>
    #main{
    padding: 1rem;
      display: flex;
      flex-direction: row; 
      justify-content: space-between; 
    }
    h1{
        font-weight: bolder;
        text-decoration: underline;
        text-decoration-color: #598502; 
        margin: 0;
    }

</style>

<!-- <h1>Agglutinative Grammar Component Test:</h1> -->
<!-- <h2>{mary} {john} </h2> -->
<div id="main"> 
    <div id="dictionary">
        <h1>Dictionary:</h1>
        <h4>*Paranthesis indicate the IPA <br/>
        transcription of each word*</h4>
        <Dictionary category="Nouns" dictionary={nouns}/>
        <Dictionary category="Pronouns" dictionary={pronouns}/>
        <Dictionary category="Adjectives" dictionary={adjectives}/>
        <Dictionary category="Verbs" dictionary={verbs}/>
    </div>
    <div id="conjugations">
        {#if grammarOrigin.name === "Japanese"}
            <Dictionary category="Particles" dictionary={affixes}/>
        {/if}
        <ConjugationTable pronouns={pronouns}/>
    </div>
</div>



<!-- <h4>{dictionary}</h4> -->