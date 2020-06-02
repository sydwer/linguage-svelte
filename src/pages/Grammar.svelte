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

// TRANSFER TO BAcKEND SCHEMA WHEN THE FINAL INFO IS DECIDED UPON
    const names = [{IPA: mary, latin: "Mary"},{IPA: john, latin: "John"}]

    const nouns = [{original:"Apple"},{original:"Bear"},{original:"Book"}, {original:"Cat"}, {original:"Dinner"}, {original:"Fish"},
        {original:"Hello"}, {original:"House"},{original:"Hunger"}, {original:"River"},{original:"Rock"}, {original:"Ten"},{original:"Tree"},
        ];
        // Original is used Headers, rather than English:, inorder to imply that the two following entries are modified versions of the first

    const verbs = [{original: "Able"},{original: "Eat"}, {original: "Enjoy"}, {original: "Die"}, {original: "Give"}, {original: "Have"}, 
        {original: "Say"}, {original: "Copula"}, {original: "Want"},{original: "Will"},
        ];
    const adjectives = [{original: "Big"}, {original: "Cute"}, {original: "Fast"}, {original: "Hungry"},
        ];

    const pronouns = [{original: "I"},{original:"We"},{original:"You"}, {original:"You all"},{original:"He"}, {original:"She"},
        {original:"It"}, {original:"They"},
        ];

   
    // const defaultNames = [{IPA: mary, latin: "Mary"},{IPA: john, latin: "John"}]

    // const defaultNouns = [{original:"Apple"},{original:"Bear"},{original:"Book"}, {original:"Cat"}, {original:"Dinner"}, {original:"Fish"},
    //     {original:"Hello"}, {original:"House"},{original:"Hunger"}, {original:"River"},{original:"Rock"}, {original:"Ten"},{original:"Tree"},
    //     ];
    //     // Original is used Headers, rather than English:, inorder to imply that the two following entries are modified versions of the first

    // const defaultVerbs = [{original: "Able"},{original: "Eat"}, {original: "Enjoy"}, {original: "Die"}, {original: "Give"}, {original: "Have"}, 
    //     {original: "Say"}, {original: "Copula"}, {original: "Want"},
    //     ];
    // const defaultAdjectives = [{original: "Big"}, {original: "Cute"}, {original: "Fast"}, {original: "Hungry"},
    //     ];

    // const defaultPronouns = [{original: "I"},{original:"We"},{original:"You"}, {original:"You all"},{original:"He"}, {original:"She"},
    //     {original:"It"}, {original:"They"},
    //     ];

    // const names = {};
    // const nouns = {};
    // const pronouns ={};
    // const verbs = {};
    // const adjectives = {};


    /////
    ////
    ///
    // ALL OF THIS IS CURRENTLY ON NEWEST BACKEND WITH IT ROUTE BEING SET UP
    //-THIS IS A PLACEHOLDER BUT NECESSARY 
    // FOR ANY FROTNEND WORK BEING DONE AS A BREAK FROM THE BACKEND DEVELOPMENT
    // DO
    // NOT 
    // DELETE 
    // IT 
    // YET
    //////
    /////
    ////
    ///
    //
    

    let test = [{original: "one"}, {original: "dos"}];

    if(syllableBank){
        makeDictionary(nouns);
        makeDictionary(verbs);
        makeDictionary(adjectives);
        makeDictionary(pronouns);
        // makeDictionary(test);
        addKeys();
    }

    function addKeys(){
        markWordTest(names);
        markWordTest(nouns);
        markWordTest(pronouns);
        markWordTest(verbs);
        // markWordTest(defaultAdjectives, adjectives);
        markWordTest(adjectives);
        markWordTest(test);
        // testTheTest();
    }
    // if(syllableBank){
    //     makeDictionary(defaultNouns);
    //     makeDictionary(defaultVerbs);
    //     makeDictionary(defaultAdjectives);
    //     makeDictionary(defaultPronouns);
    //     makeDictionary(test);
    //     addKeys();
    // }

    // function addKeys(){
    //     markWord(defaultNames, names);
    //     markWord(defaultNouns, nouns);
    //     markWord(defaultPronouns, pronouns);
    //     markWord(defaultVerbs, verbs);
    //     // markWord(defaultAdjectives, adjectives);
    //     markWordTest(defaultAdjectives);
    //     markWordTest(test);
    //     testTheTest();
    // }

    function testTheTest(){
        // console.log(adjectives)
    }

      function markWord(dictionary, newDictionary){
          dictionary.map(word =>{
              if(dictionary === names){
            //   if(dictionary === defaultNames){
                  newDictionary[word.latin.toLowerCase()] = word
            }else{
                newDictionary[word.original.toLowerCase()] = word
            }

        })
        dictionary = newDictionary;
   
    }

      function markWordTest(dictionary){
        //   let dictionary = [{}];
          dictionary.map(word =>{
              if(dictionary === names){
            //   if(dictionary === defaultNames){
                  dictionary[word.latin.toLowerCase()] = word
            }else{
                dictionary[word.original.toLowerCase()] = word
            }
                
        })
        // rework so that the dictionary only has entries with name MSMediaKeySession, not index numbers
        // dictionary.length = 0;
        // dictionary = newDictionary;
    }
       
    const standardDictionary = {names, nouns, pronouns, verbs, adjectives}
    // const testDictionary = {names, nouns, pronouns, verbs, defaultAdjectives}
    // console.log(standardDictionary)

    

    // function makeBoundMorpheme(syllables){
    //     const morpheme = syllables[Math.floor(Math.random() * syllables.length)]
    //     return morpheme
    // }

        function makeGrammar(word){
        const randomSyllable = syllableBank[Math.floor(Math.random() * syllableBank.length)];
        let IPA = randomSyllable.IPA;
        let latin = randomSyllable.latin;
        // if(word === possesive){
        //     word.IPA = "'" + IPA;
        // } else if(word === plural || word === advAdj){
        //     word.IPA = IPA
        // }
        // else{
            word.IPA = IPA;
            word.latin = latin;
        // }
    }


    function makeFreeMorpheme(syllables){
        //want 2-4 syllables so 1-3, and then add one?
        const randomSyllablesIPA = []
        const randomSyllablesLatin = []
        let syllableAmount = undefined;
        const randomNumber = Math.floor(Math.random() * 10);
        if (randomNumber === 1){
            syllableAmount = 1;
        }else if(randomNumber < 9){
            syllableAmount = 2
        }else{
            syllableAmount = 3
        }
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
            newWord = makeFreeMorpheme(syllableBank)
            dictionary[i].IPA = newWord.IPA
            dictionary[i].latin = newWord.latin
        }
    }

    /////
    ////
    ///
    //END PLACEHOLDER LOGIC
    ///
    ////
    /////

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
  
   

</style>


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
    <!-- <div id="grammar-details"></div> -->
    {#if grammarOrigin.name === "English"}
        <English  dictionary={standardDictionary} makeGrammar={makeGrammar} markWord={markWordTest}/>
    {:else if grammarOrigin.name === "German"}
        <German dictionary={standardDictionary} makeGrammar={makeGrammar} markWord={markWordTest}/>
    {:else}
    <br>
    <br>
    <br>
    <h2> 
    Oops! Looks like this grammar option is under construction, 
    check back soon for an update!
    </h2>
    {/if}
    </div>
</div>



