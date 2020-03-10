<script>
// import {onMount } from 'svelte'
import Dictionary from './Dictionary.svelte'
import ConjugationTable from './ConjugationTable.svelte'
import Sentances from './Sentances.svelte'
import German from './grammars/German.svelte'
import English from './grammars/English.svelte'

export let syllableBank;
export let mary;
export let john;
export let grammarOrigin;


    // const maryName = {IPA: mary, latin: "Mary"};
    // const johnName = {IPA: john, latin: "John"}
    // const names = {mary: maryName, john: johnName}
    const names = [{IPA: mary, latin: "Mary"},{IPA: john, latin: "John"}]



    // const nouns = [{apple:{original: "Apple", IPA: undefined, latin: undefined}},{bear:{original: "Bear", IPA: undefined, latin: undefined}},
    //     {book:{original: "Book", IPA: undefined, latin: undefined}}, {cat:{original: "Cat", IPA: undefined, latin: undefined}}, 
    //     {dinner:{original: "Dinner", IPA: undefined, latin: undefined}}, {fish:{original: "Fish", IPA: undefined, latin: undefined}},
    //     {hello:{original: "Hello", IPA: undefined, latin: undefined}}, {house:{original: "House", IPA: undefined, latin: undefined}},
    //     {hunger:{original: "Hunger", IPA: undefined, latin: undefined}}, {river:{original: "River", IPA: undefined, latin: undefined}},
    //     {rock:{original: "Rock", IPA: undefined, latin: undefined}}, {ten:{original: "Ten", IPA: undefined, latin: undefined}},
    //     {tree:{original: "Tree", IPA: undefined, latin: undefined}},
    //     ];
    const nouns = [{original:"Apple"},{original:"Bear"},{original:"Book"}, {original:"Cat"}, {original:"Dinner"}, {original:"Fish"},
        {original:"Hello"}, {original:"House"},{original:"Hunger"}, {original:"River"},{original:"Rock"}, {original:"Ten"},{original:"Tree"},
        ];


    // const nouns = [{original: "Apple", IPA: undefined, latin: undefined},{original: "Bear", IPA: undefined, latin: undefined},
    //     {original: "Book", IPA: undefined, latin: undefined}, {original: "Cat", IPA: undefined, latin: undefined}, 
    //     {original: "Dinner", IPA: undefined, latin: undefined}, {original: "Fish", IPA: undefined, latin: undefined},
    //     {original: "Hello", IPA: undefined, latin: undefined}, {original: "House", IPA: undefined, latin: undefined},
    //     {original: "Hunger", IPA: undefined, latin: undefined}, {original: "River", IPA: undefined, latin: undefined},
    //     {original: "Rock", IPA: undefined, latin: undefined}, {original: "Ten", IPA: undefined, latin: undefined},
    //     {original: "Tree", IPA: undefined, latin: undefined},
    //     ];
        // Original is used Headers, rather than English:, inorder to imply that the two following entries are modified versions of the first

    const verbs = [{original: "Able To"},{original: "Eat"}, {original: "Enjoy"}, {original: "Die"}, {original: "Give"}, {original: "Have"}, 
        {original: "Say"}, {original: "To Be"}, {original: "Want"},
        ];
    const adjectives = [{original: "Big"}, {original: "Cute"}, {original: "Fast"}, {original: "Hungry"},
        ];

    const pronouns = [{original: "I"},{original:"We"},{original:"You"}, {original:"You all"},{original:"He"}, {original:"She"},
        {original:"It"}, {original:"They"},
        ];

    const tenses =[{original: "Past"},{original: "Present"},{original: "Future"}, {original: "Imperfect"},
        {original: "Conditional"},
        ];
    
    const particles =[{original: "Topic"},{original:"Subject"},{original: "Object"},{original: "Also/Too"},{original: "To/From/By"}, {original: "Location/At"},
        {original: "And"},{original: "Possesive"},{original: "Question Marker"},
        ];
    
    const cases = [{original: "Nominative"},{original: "Accusative"},{original: "Dative"},{original: "Genative"},
        ];

    const genders = [{original: "Masculine"},{original: "Feminine"},{original: "Neutral"},{original: "Plural"},
        ];

    const classes = [{original: "People"}, {original: "Inanimate Objects"},{original: "Names and Kinship Terms"}, 
        {original: "Round Objects"},{original: "Food"}, {original: "Tools"},{original: "Countable Items"}, 
        {original: "Infinitive Verbs"},{original: "Known Location"}, {original: "Ambiguous Location"},
        {original: "Location in Relation to Another Object"},
        ];

    const determiners = [{original: "The"},{original: "A"},{original: "Adverb Marker"},
    ];
    // ^^^Sort alphabetically and by part of speech^^^// 
    if(syllableBank){
        makeDictionary(nouns);
        makeDictionary(verbs);
        makeDictionary(adjectives);
        makeDictionary(pronouns);
        makeDictionary(tenses);
        makeDictionary(cases);
        makeDictionary(genders);
        makeDictionary(determiners);
        // makeDictionary(classes);
        if(grammarOrigin.name === "Japanese"){
            makeDictionary(particles);
        }
        if(grammarOrigin.name === "Swahili"){
            makeDictionary(classes)
        }
    }
       

    const dictionary = {names, nouns, pronouns, verbs, adjectives}

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
            // if (dictionary === pronouns || dictionary === particles || dictionary === cases || dictionary === genders || dictionary === determiners){
            if(dictionary !== nouns || dictionary !== verbs || dictionary !== adjectives){
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
        padding-right: 2rem;
        display: flex;
        flex-direction: column;
        align-items: center;
        /* justify-content: space-between; */
    }
    #dictionary{
        padding-left: 1rem;
    }
    h1{
        font-weight: bolder;
        /* text-decoration: underline;
        text-decoration-color: #598502;  */
        color: #598502;
        text-decoration: underline;
        margin: 0;
    }
    #sentances>h2{
        display: flex;
        justify-content: center;
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
        <Dictionary category="Other" dictionary={determiners}/>
    </div>
    <div id="grammar">
    <h1>Basic Grammar:</h1>
    <!-- <div id="grammar-details"></div> -->
    {#if grammarOrigin.name === "English"}
        <English syllables={syllableBank} dictionary={dictionary}/>
    {:else}
    <!-- Place holder grammar- delete once specialized fiels all built -->
        {#if grammarOrigin.name === "Japanese"}
           
            <h2>Particles:</h2>
            <ConjugationTable allInfo={particles} columns= "1"/>
            
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
        {#if grammarOrigin.name === "German" || grammarOrigin.name === "Korean"}
        <h2>Grammatical Cases:</h2>
            <ConjugationTable allInfo={cases} columns="1"/>
        {/if}
        <br/>
        <br/>
    <div id="sentances">
        <h2>Sample Sentences:</h2>
        <Sentances names={names} nouns={nouns} verbs={verbs} adjectives={adjectives} tenses={tenses} genders={genders} 
        <!-- cases={cases} determiners={determiners} pronouns={pronouns}/> 

    </div>
    <!-- delete this once special grammar files all made -->
    {/if}
    </div>
</div>



<!-- <h4>{dictionary}</h4> -->