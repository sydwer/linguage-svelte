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

    const tenses =[{original: "Past", IPA: undefined, latin: undefined},{original: "Present", IPA: undefined, latin: undefined},
        {original: "Future", IPA: undefined, latin: undefined}, {original: "Imperfect", IPA: undefined, latin: undefined},
        {original: "Conditional", IPA: undefined, latin: undefined},
        ];
    
    const particles =[{original: "Topic", IPA: undefined, latin: undefined},{original:"Subject", IPA: undefined, latin: undefined},
        {original: "Object", IPA: undefined, latin: undefined},{original: "Also/Too", IPA: undefined, latin: undefined},
        {original: "To/From/By", IPA: undefined, latin: undefined}, {original: "Location/At", IPA: undefined, latin: undefined},
        {original: "And", IPA: undefined, latin: undefined},{original: "Possesive", IPA: undefined, latin: undefined},
        {original: "Question Marker", IPA: undefined, latin: undefined},]
    
    const cases = [{original: "Nominative", IPA: undefined, latin: undefined},{original: "Accusative", IPA: undefined, latin: undefined},
        {original: "Dative", IPA: undefined, latin: undefined},{original: "Genative", IPA: undefined, latin: undefined},
        ];

    const genders = [{original: "Masculine", IPA: undefined, latin: undefined},{original: "Feminine", IPA: undefined, latin: undefined},
        {original: "Neutral", IPA: undefined, latin: undefined},
        ];

    const classes = [{original: "People", IPA: undefined, latin: undefined}, {original: "Inanimate Objects", IPA: undefined, latin: undefined},
        {original: "Names and Kinship Terms", IPA: undefined, latin: undefined},{original: "Round Objects", IPA: undefined, latin: undefined},
        {original: "Food", IPA: undefined, latin: undefined}, {original: "Tools", IPA: undefined, latin: undefined},
        {original: "Countable Items", IPA: undefined, latin: undefined}, {original: "Infinitive Verbs", IPA: undefined, latin: undefined},
        {original: "Known Location", IPA: undefined, latin: undefined}, {original: "Ambiguous Location", IPA: undefined, latin: undefined},
        {original: "Location in Relation to Another Object", IPA: undefined, latin: undefined},
        ];
    // ^^^Sort alphabetically and by part of speech^^^// 
    if(syllableBank){
        makeDictionary(nouns);
        makeDictionary(verbs);
        makeDictionary(adjectives);
        makeDictionary(pronouns);
        makeDictionary(tenses);
        makeDictionary(cases);
        if(grammarOrigin.name === "Japanese"){
            makeDictionary(particles);
        }
        if(grammarOrigin.name === "Swahili"){
            makeDictionary(classes)
        }
        if(grammarOrigin.noun_classes > 0 && grammarOrigin.name !== "Swahili"){
            makeDictionary(genders)
        }
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
            if (dictionary=== pronouns || dictionary === particles || dictionary === cases){
                newWord = makeBoundMorpheme(syllableBank)
            }else{
                newWord = makeFreeMorpheme(syllableBank)
            }
            dictionary[i].IPA = newWord.IPA
            dictionary[i].latin = newWord.latin
        }
        // console.log(tenses)
    }

</script>

<style>
    #main{
        width: 100%;
        padding: 1rem;
        padding-left: 0;
        display: grid;
        grid-template-columns: 1fr 2fr; 
    }
    #grammar{
        padding-right: 1rem;
        display: flex;
        flex-direction: column;
        align-items: center;
        /* justify-content: space-between; */
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
    <div id="grammar">
    <h1>Basic Grammar:</h1>
    <div id="grammar-details"></div>
        {#if grammarOrigin.name === "Japanese"}
            <Dictionary category="Particles" dictionary={particles}/>
            <p>*Add these onto the end of a word to mark
                <br>its role in the sentance
            </p>
        {/if}
        <h2>Pronouns:</h2>
        <ConjugationTable allInfo={pronouns} columns="2"/>
        <br/>
          {#if grammarOrigin.noun_classes > 0}
        <h2>Noun Classes/Genders:</h2>
        {#if grammarOrigin.noun_classes === 2}
            <ConjugationTable allInfo={genders} columns="-2"/>
        {:else if grammarOrigin.name === "German"}
            <ConjugationTable allInfo={genders} columns="1"/>
        {:else if grammarOrigin.name === "Swahili"}
            <ConjugationTable allInfo={classes} columns="1"/>
        {:else}
            <ConjugationTable allInfo={genders} columns="1"/>
        {/if}
        {/if}
        <br/>
        <h2>Conjugation Table:</h2>
        {#if grammarOrigin.name === "Japanese"}
            <ConjugationTable allInfo={tenses} columns="-1"/>
        {:else}
            <ConjugationTable allInfo={tenses} columns="1"/>
        {/if}
        <!-- {#if grammarOrigin.noun_classes > 0}
        <h2>Noun Classes/Genders:</h2>
        {#if grammarOrigin.noun_classes === 2}
            <ConjugationTable allInfo={genders} columns="-2"/>
        {:else if grammarOrigin.name === "German"}
            <ConjugationTable allInfo={genders} columns="1"/>
        {:else if grammarOrigin.name === "Swahili"}
            <ConjugationTable allInfo={classes} columns="1"/>
        {:else}
            <ConjugationTable allInfo={genders} columns="1"/>
        {/if}
        {/if} -->
        {#if grammarOrigin.name === "German"}
        <h2>Grammatical Cases:</h2>
            <ConjugationTable allInfo={cases} columns="1"/>
        {/if}

    </div>
</div>
<div id="sentances">
</div>



<!-- <h4>{dictionary}</h4> -->