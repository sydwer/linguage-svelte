<script>
import ConjugationTable from '../ConjugationTable.svelte'
export let dictionary;
export let makeGrammar;
export let markWord;
/////
////
///
//this is all going away once the new backend is built/properly linked up- placeholder for
// now for work breaks involving the front end/taking breaks to do some design
// between designing the database
///
////
/////

    const names = dictionary.names;
    const nouns = dictionary.nouns;
    const pronouns = dictionary.pronouns;
    const verbs = dictionary.verbs;
    const adjectives = dictionary.adjectives;
    // const adjectives = dictionary.defaultAdjectives;
// GRAMMAR DICTIONARIES
    const possesive = {original:"Possesive", latin:"'s", IPA: "s"};
    const plural = {original: "Plural", latin: "s", IPA: "s"};
    const advAdj = {original: "Adverb/Adjective", latin: "y", IPA: "i"};
    const casePronouns = [{original: "Me"},{original: "Him"}, 
        {original: "Her"},{original: "Them"},{original: "My"},{original: "Your"},
        {original: "His"},{original: "Hers"},{original: "Their"}
    ];
    // const  casePronouns = {};
    const prepositions = [{original: "Around"},{original: "By"},{original: "From"},
    {original: "To"},{original: "Through"},{original: "Toward"}
    ];
    // const prepositions = {};

    const tenses =[{original: "Past"},{original: "Present"}
    ];
    // const tenses = {};

    const helperVerbs =[{original: "Future"}, {original: "Imperfect"}, 
    {original: "Conditional"}
    ];
    // const helperVerbs ={};

    const determiners = [{original: "The"}, {original: "A"},{original: "This"}, {original: "That"}
    ,]
    // const determiners = {};
    const englishGrammar = [prepositions,tenses,helperVerbs,determiners, casePronouns]

    // function makeGrammar(word){
    //     const randomSyllable = syllables[Math.floor(Math.random() * syllables.length)];
    //     let IPA = randomSyllable.IPA;
    //     let latin = randomSyllable.latin;
    //     // if(word === possesive){
    //     //     word.IPA = "'" + IPA;
    //     // } else if(word === plural || word === advAdj){
    //     //     word.IPA = IPA
    //     // }
    //     // else{
    //         word.IPA = IPA;
    //         word.latin = latin;
    //     // }
    // }

   function makeEnglishGrammarDictionaries(){
       englishGrammar.map(grammarTrait =>{
           grammarTrait.map(makeGrammar);
       })
   }
    // tenses.map(makeGrammar);
    // helperVerbs.map(makeGrammar);
    // determiners.map(makeGrammar);
    // casePronouns.map(makeGrammar);
    // prepositions.map(makeGrammar);
    const endings = [possesive,plural,advAdj];
   
    
    
    // function markWord(dictionary, newDictionary){
    //     dictionary.map(word =>{
    //         if(dictionary === oldNames){
    //             newDictionary[word.latin.toLowerCase()] = word
    //         }else{
    //             newDictionary[word.original.toLowerCase()] = word
    //         }

    //     })
    // }


    function addKeysToGrammar(){
        englishGrammar.map(dictionary =>{
            markWord(dictionary)
        })
    }
    // markWord(tenses);
    // markWord(helperVerbs);
    // markWord(determiners);
    // markWord(casePronouns);
    // markWord(prepositions);

    function makeEnglishGrammar(){
        makeEnglishGrammarDictionaries();
        addKeysToGrammar();
    }

    makeEnglishGrammar();

    /////
    ////
    ///
    //End logic- everything above here can be deleted upon new backend being finished 
    // (oh my god the amount of join tables is dumb why did i do that to myself)
    ///
    ////
    /////
  

   
    

</script>


<style>
div{
    width: 100%;
    border-bottom: 2px solid grey
}
h4{
    width: 100%;
    display: flex;
    justify-content: space-evenly;
}

</style>


<h2>Verb Endings</h2>
<ConjugationTable allInfo={tenses} columns="1"/>
<br/>
<h2>"Helper Verbs"</h2>
<ConjugationTable allInfo={helperVerbs} columns="1"/>
<br/>
<h2>Useful Noun Endings</h2>
<ConjugationTable allInfo={endings} columns="1"/>
<br/>
<h2>Prepositions</h2>
<ConjugationTable allInfo={prepositions} columns="1"/>
<br/>
<!-- <h2>Verb Endings</h2>
<ConjugationTable allInfo={oldTenses} columns="1"/>
<h2>"Helper Verbs"</h2>
<ConjugationTable allInfo={oldHelperVerbs} columns="1"/>
<h2>Useful Noun Endings</h2>
<ConjugationTable allInfo={endings} columns="1"/>
<h2>Prepositions</h2>
<ConjugationTable allInfo={oldPrepositions} columns="1"/> -->


<h2> Sample Sentences:</h2>
<div>
    <h4>
        <span>{names.mary.IPA}</span> <span>{verbs.say.IPA}-{tenses.present.IPA}</span> 
        <span>"{nouns.hello.IPA}"</span>
    </h4>

    <h4>
        <span>{names.mary.latin}</span> <span>{verbs.say.latin}-{tenses.present.latin}</span> 
        <span>"{nouns.hello.latin}"</span>
    </h4>

    <h4><span>Mary</span> <span>say-PRES</span> <span>"hello"</span></h4>
    
    <h4>'Mary says "hello".'</h4>
    <!-- Spans are ugly here, but necessary if I want the proper 'words should be lined up with what they  -->
    <!-- reference convention of linguistics ' -->
</div>
<div>
    <h4>
        <span>{determiners.the.IPA}</span><span>{nouns.tree.IPA}</span><span>{verbs.die.IPA}-
        {tenses.past.IPA}</span>
    </h4>

    <h4>
        <span>{determiners.the.latin}</span><span>{nouns.tree.latin}</span><span>{verbs.die.latin}-
        {tenses.past.latin}</span>
    </h4>

    <h4><span>DET</span><span>tree</span><span>die-PAST</span></h4>

    <h4>'The tree died.'</h4>
</div>
<div>
    <h4>
        <span>{determiners.the.IPA}</span><span>{nouns.cat.IPA}-{plural.IPA}</span>{helperVerbs.future.IPA}
        <span>{verbs.eat.IPA}</span><span>{nouns.fish.IPA}</span>
    </h4>
    <h4>
        <span>{determiners.the.latin}</span><span>{nouns.cat.latin}-{plural.latin}</span>{helperVerbs.future.latin}
        <span>{verbs.eat.latin}</span><span>{nouns.fish.latin}</span>
    </h4>
    <h4>
        <span>DET</span><span>cat-PL</span>will<span>eat</span><span>fish.PL</span>
    </h4>
    <h4> 'The cats will eat fish.'</h4>
</div>
<div>
    <h4>
        <span>{pronouns.we.IPA}</span><span>{verbs.copula.IPA}</span>
        <span>{nouns.hunger.IPA}{advAdj.IPA}</span>
    </h4>
    <h4>
        <span>{pronouns.we.latin}</span><span>{verbs.copula.latin}</span>
        <span>{nouns.hunger.latin}{advAdj.latin}</span>
    </h4>
    <h4>
        <span>1sg.PL</span><span>to be</span><span>hungry</span>
    </h4>
    <h4>'We're hungry.'</h4>
</div>
<div>
    <h4>
        <span>{pronouns.i.IPA}</span><span>{helperVerbs.conditional.IPA}</span>
        <span>{verbs.give.IPA}</span><span>{casePronouns.him.IPA}</span><span>{casePronouns.my.IPA}</span>
        <span>{nouns.book.IPA}</span>
    </h4>
    <h4>
        <span>{pronouns.i.latin}</span><span>{helperVerbs.conditional.latin}</span>
        <span>{verbs.give.latin}</span><span>{casePronouns.him.latin}</span><span>{casePronouns.my.latin}</span>
        <span>{nouns.book.latin}</span>
    </h4>
    <h4>
        <span>1sg.NOM</span><span>would</span><span>give</span>
        <span>3sg.MASC.DAT</span><span>1sg.POSS</span><span>book</span>
    </h4>
    <h4>'I would give him my book.'</h4>
</div>
<div>
    <h4>
        <span>{pronouns.i.IPA}</span><span>{verbs.want.IPA}-{tenses.past.IPA}</span>
        <span>{determiners.a.IPA}</span><span>{nouns.rock.IPA}</span>
        <span>{prepositions.from.IPA}</span><span>{determiners.the.IPA}</span>
        <span>{nouns.river.IPA}</span>
    </h4>
    <h4>
        <span>{pronouns.i.latin}</span><span>{verbs.want.latin}-{tenses.past.latin}</span>
        <span>{determiners.a.latin}</span><span>{nouns.rock.latin}</span>
        <span>{prepositions.from.latin}</span><span>{determiners.the.latin}</span>
        <span>{nouns.river.latin}</span>
    </h4>
    <h4>
        <span>1sg.NOM</span><span>want-PAST</span><span>ART</span><span>rock</span>
        <span>from</span><span>DET</span><span>river</span>
    </h4>
    <h4>'I wanted a rock from the river.'</h4>
</div>
<div>
    <h4>
        <span>{determiners.a.IPA}</span><span>{adjectives.big.IPA}</span>
        <span>{nouns.bear.IPA}</span><span>{verbs.able.IPA}{helperVerbs.imperfect.IPA}</span>
        <span>{verbs.eat.IPA}</span><span>{nouns.ten.IPA}</span><span>{nouns.fish.IPA}</span>
        <span>{adjectives.fast.IPA}-{advAdj.IPA}</span>
    </h4>
    <h4>
        <span>{determiners.a.latin}</span><span>{adjectives.big.latin}</span>
        <span>{nouns.bear.latin}</span><span>{verbs.able.latin}{helperVerbs.imperfect.latin}</span>
        <span>{verbs.eat.latin}</span><span>{nouns.ten.latin}</span><span>{nouns.fish.latin}</span>
        <span>{adjectives.fast.latin}-{advAdj.latin}</span>
    </h4>
    <h4>
        <span>ART</span><span>big</span><span>bear</span>
        <span>able.COND</span><span>eat</span><span>ten</span>
        <span>fish.PL</span><span>quick-ADV</span>
    </h4>
    <h4>'A big bear could eat 10 fish quickly.'</h4>
</div>
 