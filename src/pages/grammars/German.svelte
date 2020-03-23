<script>
import ConjugationTable from '../ConjugationTable.svelte'
import GermanGrammarTable from '../tables/GermanGrammarTable.svelte'
export let dictionary;
export let makeGrammar;
export let markWord;


const names = dictionary.names;
const nouns = dictionary.nouns;
const verbs = dictionary.verbs;
const adjectives = dictionary.adjectives;

// There's a ton of cases markers in German, come back if figuring out a more concide way of doing this
const mascDet = [{original: "Nominative"},{original: "Accusative"},{original: "Dative"},
{original: "Genitive"},];

const femDet = [{original: "Nominative"},{original: "Accusative"},{original: "Dative"},
{original: "Genitive"},];

const neutDet = [{original: "Nominative"},{original: "Accusative"},{original: "Dative"},
{original: "Genitive"},];

const plDet = [{original: "Nominative"},{original: "Accusative"},{original: "Dative"},
{original: "Genitive"},];

const mascArt = [{original: "Nominative"},{original: "Accusative"},{original: "Dative"},
{original: "Genitive"},];

const femArt = [{original: "Nominative"},{original: "Accusative"},{original: "Dative"},
{original: "Genitive"},];

const neutArt = [{original: "Nominative"},{original: "Accusative"},{original: "Dative"},
{original: "Genitive"},];

const plArt = [{original: "Nominative"},{original: "Accusative"},{original: "Dative"},
{original: "Genitive"},];

const nomEndings = [{original: "Masculine"},{original: "Feminine"},{original: "Neutral"},
{original: "Plural"},];

const accEndings = [{original: "Masculine"},{original: "Feminine"},{original: "Neutral"},
{original: "Plural"},];

const datEndings = [{original: "Masculine"},{original: "Feminine"},{original: "Neutral"},
{original: "Plural"},];

const genEndings = [{original: "Masculine"},{original: "Feminine"},{original: "Neutral"},
{original: "Plural"},];

const nomPronouns = [{original: "I"},{original: "We"},{original: "You"},
{original:"You_all"},{original:"He"},{original:"She"},{original:"It"},
{original:"They"},];

const accPronouns = [{original: "I"},{original: "We"},{original: "You"},
{original:"You_all"},{original:"He"},{original:"She"},{original:"It"},
{original:"They"},];

const datPronouns = [{original: "I"},{original: "We"},{original: "You"},
{original:"You_all"},{original:"He"},{original:"She"},{original:"It"},
{original:"They"},];

const genPronouns = [{original: "I"},{original: "We"},{original: "You"},
{original:"You_all"},{original:"He"},{original:"She"},{original:"It"},
{original:"They"},];

const pronouns = {nom: nomPronouns, acc: accPronouns, dat: datPronouns, gen: genPronouns};

const cases = [mascDet, femDet, neutDet, plDet, mascArt, femArt, neutArt, plArt, 
nomEndings, accEndings, datEndings, genEndings];
// Det is determiners('the'), and Art is articles('a' or 'an')
// See if this is better for using in making SVGElementInstanceList, otehrwise get rid of it ^^

const presentTenses =[{original: "I"},{original:"We"},{original:"You"},{original:"You_All"},
{original: "He/She/It"},{original:"They"},];

const pastTenses =[{original: "I"},{original:"We"},{original:"You"},{original:"You_All"},
{original: "He/She/It"},{original:"They"},];

const prepositions = [{original: "By"}, {original: "Through"}, {original: "Along"}, {original: "For"}, {original: "Against"},
{original: "Towards"}, {original: "Without"},{original: "About"},];



const germanGrammar = [mascDet, femDet, neutDet, plDet, mascArt, femArt, neutArt, plArt, 
nomEndings, accEndings, datEndings, genEndings, presentTenses, pastTenses, prepositions,
nomPronouns, accPronouns, datPronouns, genPronouns];

function makeGrammarDictionaries(){
  germanGrammar.map(dictionary=>{
    dictionary.map(makeGrammar)
  })
  // prepositions.map(makeGrammar);
  // cases.map(caseType => {
  //   caseType.map(makeGrammar)
  // })
}

function makeKeys(){
  germanGrammar.map(dictionary=>{
    markWord(dictionary)
  })
  // markWord(prepositions);
  // cases.map(caseType => {
  //   markWord(caseType)
  // })
}

function makeGermanGrammar(){
  makeGrammarDictionaries();
  makeKeys();
}

makeGermanGrammar();
console.log(pronouns)

</script>


<style>
</style>
<h2>Present Tense Verb Endings:</h2>
<ConjugationTable allInfo={presentTenses} columns="2"/>
<br>
<h2>Past Tense Verb Endings:</h2>
<ConjugationTable allInfo={pastTenses} columns="2"/>
<br>
<h2>Pronouns (by Grammatical Case):</h2>
<GermanGrammarTable pronouns={pronouns}/>
<br>
<!-- verb kickers, multiple clauses are a must, so is dat/acc verbs and movement/stationary past. -->
<!-- include nach vs zu example -->

<!-- Change nouns and verbs so the sentences are different from other langs -->

 <!-- <h4>'A big bear could eat 10 fish quickly.'</h4>
     <h4>'I wanted a rock from the river.'</h4>
    <h4>'I would give him my book.'</h4>
    <h4> 'We're hungry.'</h4>
      <h4>'The cats will eat fish.'</h4>
    <h4>'The tree died.'</h4>
    <h4>'Mary says "hello".'</h4> -->