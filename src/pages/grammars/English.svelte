<script>
import ConjugationTable from '../ConjugationTable.svelte'
export let syllables;
export let dictionary;

const oldNouns = dictionary.nouns;  
const nouns = {}; 
const oldPronouns = dictionary.pronouns;
const pronouns ={};   
const oldVerbs = dictionary.verbs;   
const verbs ={};
const oldAdjectives = dictionary.adjectives; 
const adjectives = {};  
const oldNames = dictionary.names;  
const names = {}; 

// GRAMMAR DICTIONARIES
    const possesive = {original:"Possesive", latin:"'s"};
    const plural = {original: "Plural", latin: "s"};

    const oldTenses =[{original: "Past"},{original: "Present"}
    ];
    const tenses = {};
    const oldHelperVerbs =[{original: "Future"}, {original: "Imperfect"}, 
    {original: "Conditional"}
    ];
    const helperVerbs ={};
    const oldDeterminers = [{original: "The"}, {original: "A"},{original: "This"}, {original: "That"}
    ,]
    const determiners = {};


    function makeGrammar(word){
        const randomSyllable = syllables[Math.floor(Math.random() * syllables.length)];
        let IPA = randomSyllable.IPA;
        let latin = randomSyllable.latin;
        if(word === possesive){
            word.IPA = "'" + IPA;
        } else if(word === plural){
            word.IPA = IPA
        }
        else{
            word.IPA = IPA;
            word.latin = latin;
        }
    }

    makeGrammar(possesive);
    makeGrammar(plural);
    const endings = [possesive,plural];
    oldTenses.map(makeGrammar);
    oldHelperVerbs.map(makeGrammar);
    oldDeterminers.map(makeGrammar);
    
    
    function markWord(dictionary, newDictionary){
        dictionary.map(word =>{
            if(dictionary === oldNames){
                newDictionary[word.latin.toLowerCase()] = word
            }else{
                newDictionary[word.original.toLowerCase()] = word
            }

        })
    }

    markWord(oldTenses,tenses);
    markWord(oldNouns,nouns);
    markWord(oldPronouns,pronouns);
    markWord(oldAdjectives,adjectives);
    markWord(oldNames,names);
    markWord(oldVerbs,verbs);
    markWord(oldHelperVerbs,helperVerbs);
    markWord(oldDeterminers, determiners);

   
    

</script>


<style>
div{
    width: 100%
}
h4{
    width: 100%;
    display: flex;
    justify-content: space-evenly;
}
</style>
<h2>Verb Endings</h2>
<ConjugationTable allInfo={oldTenses} columns="1"/>
<h2>"Helper Verbs"</h2>
<ConjugationTable allInfo={oldHelperVerbs} columns="1"/>
<h2>Useful Noun Endings</h2>
<ConjugationTable allInfo={endings} columns="1"/>

<h2> Sample Sentances:</h2>
<div>
    <h4><span>{names.mary.latin}</span> <span>{verbs.say.latin}{tenses.present.latin}</span> 
    <span>"{nouns.hello.latin}"</span></h4>

    <h4><span>{names.mary.IPA}</span> <span>{verbs.say.IPA}{tenses.present.IPA}</span> 
    <span>"{nouns.hello.IPA}"</span></h4>

    <h4><span>Mary</span> <span>say.PRES</span> <span>"hello"</span></h4>
    
    <h4>'Mary says "hello".'</h4>
    <!-- Spans are ugly here, but necessary if I want the proper 'words should be lined up with what they  -->
    <!-- reference convention of linguistics ' -->
</div>