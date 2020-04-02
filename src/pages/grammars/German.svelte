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



// function createSubjunctive(){
//   let become = verbs.find(o => o.original === "Will");
//   become.original = "Become"
// }


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

// endings is the grammar for the end of adjectives and articles to match gender and case of word they midify
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

const possPronouns = [{original: "I"},{original: "We"},{original: "You"},
{original:"You_all"},{original:"He"},{original:"She"},{original:"It"},
{original:"They"},];

const pronouns = {nom: nomPronouns, acc: accPronouns, dat: datPronouns, gen: genPronouns};

const cases = [mascDet, femDet, neutDet, plDet, mascArt, femArt, neutArt, plArt, 
nomEndings, accEndings, datEndings, genEndings];
// Det is determiners('the'), and Art is articles('a' or 'an')
// See if this is better for using in making SVGElementInstanceList, otehrwise get rid of it ^^

const presentTenses =[{original: "I"},{original:"We"},{original:"You"},{original:"You_All"},
{original: "He_She_It"},{original:"They"},];

const subjunctive = [{original: "Become"}]

// const pastTenseSuffix =[{original: "I"},{original:"We"},{original:"You"},{original:"You_All"},
// {original: "He_She_It"},{original:"They"},];

// const pastTensePrefixes =[{original: "I"},{original:"We"},{original:"You"},{original:"You_All"},
// {original: "He_She_It"},{original:"They"},];
const pastTenseAffixes =[{original: "Prefix"},{original: "Suffix"}];

const prepositions = [{original: "By"}, {original: "Through"}, {original: "Along"}, {original: "For"}, {original: "Against"},
{original: "Towards"}, {original: "Without"},{original: "About"},];


const adverb = {original: "Adverb"}


const germanGrammar = [mascDet, femDet, neutDet, plDet, mascArt, femArt, neutArt, plArt, 
nomEndings, accEndings, datEndings, genEndings, presentTenses, pastTenseAffixes, prepositions,
nomPronouns, accPronouns, datPronouns, genPronouns,possPronouns, subjunctive];

function makeGrammarDictionaries(){
  makeGrammar(adverb);
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


<h2>Present Tense Verb Endings:</h2>
<ConjugationTable allInfo={presentTenses} columns="2"/>
<br>
<h2>Past Tense Verb Prefix and suffix:</h2>
<ConjugationTable allInfo={pastTenseAffixes} columns="2"/>
<br>
<h2>Pronouns (by Grammatical Case):</h2>
<GermanGrammarTable pronouns={pronouns}/>
<br>
<br>
<h2> Sample Sentences: </h2>
<br>
<div>
  <h4>
    <span>{names.mary.IPA}</span> <span>{verbs.say.IPA}-{presentTenses.he_she_it.IPA}</span> 
    <span>"{nouns.hello.IPA}"</span>
  </h4>
  <h4>
    <span>{names.mary.latin}</span> <span>{verbs.say.latin}-{presentTenses.he_she_it.latin}</span> 
    <span>"{nouns.hello.latin}"</span>
  </h4>
  <h4>
    <span>Mary</span> <span>say-PRES</span> <span>"hello"</span>
  </h4>
  <h4>'Mary says "hello".'</h4>
</div>
<div>
  <h4>
    <span>{mascDet.nominative.IPA}</span><span>{nouns.tree.IPA}</span>
    <span>{verbs.copula.IPA}-{presentTenses.he_she_it.IPA}</span>
    <span>{pastTenseAffixes.prefix.IPA}-{verbs.die.IPA}-{pastTenseAffixes.suffix.IPA}</span>
  </h4>
  <h4>
    <span>{mascDet.nominative.latin}</span><span>{nouns.tree.latin}</span>
    <span>{verbs.copula.latin}-{presentTenses.he_she_it.latin}</span>
    <span>{pastTenseAffixes.prefix.latin}-{verbs.die.latin}-{pastTenseAffixes.suffix.latin}</span>
  </h4>
  <h4>
    <span>the.MASC.NOM</span><span>tree</span>
    <span>to be-PRES.3SG</span><span>PAST-die-PAST</span>
  </h4>
  <h4>'The tree died.'</h4>
</div>
<div>
  <h4>
    <span>{plDet.nominative.IPA}</span><span>{nouns.cat.IPA}-s</span>
    <span>{verbs.will.IPA}-{presentTenses.he_she_it.IPA}</span>
    <span>{plArt.accusative.IPA}</span><span>{nouns.fish.IPA}</span>
    <span>{pastTenseAffixes.prefix.IPA}-{verbs.eat.IPA}-{pastTenseAffixes.suffix.IPA}</span>
  </h4>
  <h4>
    <span>{plDet.nominative.latin}</span><span>{nouns.cat.latin}-s</span>
    <span>{verbs.will.latin}-{presentTenses.he_she_it.latin}</span>
    <span>{plArt.accusative.latin}</span><span>{nouns.fish.latin}</span>
    <span>{pastTenseAffixes.prefix.latin}-{verbs.eat.latin}-{pastTenseAffixes.suffix.latin}</span>
  </h4>
  <h4>
    <span>the.PL.NOM</span><span>cat-PL</span>
    <span>will-PRES.3SG</span><span>PL.ACC</span><span>fish</span>
    <span>PAST-eat-PAST</span>
  </h4>
  <h4>'The cats will eat fish.'</h4>
</div>
<div>
  <h4>
    <span>{nomPronouns.we.IPA}</span><span>{verbs.copula.IPA}-{presentTenses.we.IPA}</span>
    <span>{nouns.hunger.IPA}.{adverb.IPA}</span>
  </h4>
  <h4>
    <span>{nomPronouns.we.latin}</span><span>{verbs.copula.latin}-{presentTenses.we.latin}</span>
    <span>{nouns.hunger.latin}.{adverb.latin}</span>
  </h4>
  <h4>
    <span>we.NOM</span><span>to be-PRES.3SG</span>
    <span>hunger.ADV</span>
  </h4>
  <h4> 'We're hungry.'</h4>
</div>
<div>
  <h4>
    <span>{nomPronouns.i.IPA}</span>
    <span>{pastTenseAffixes.prefix.IPA}-{subjunctive.become.IPA}-{pastTenseAffixes.suffix.IPA}</span>
    <span>{datPronouns.he.IPA}</span><span>{possPronouns.i.IPA}-{accEndings.neutral.IPA}</span>
    <span>{nouns.book.IPA}</span>
  </h4>
  <h4>
    <span>{nomPronouns.i.latin}</span>
    <span>{pastTenseAffixes.prefix.latin}-{subjunctive.become.latin}-{pastTenseAffixes.suffix.latin}</span>
    <span>{datPronouns.he.latin}</span><span>{possPronouns.i.latin}-{accEndings.neutral.latin}</span>
    <span>{nouns.book.latin}</span>
  </h4>
  <h4>
    <span>i</span>
    <span>PAST-become-PAST</span>
    <span>he.DAT</span><span>i.POSS-ACC.NEUT</span>
    <span>book</span>
  </h4>
  <h4>'I would give him my book.'</h4>
</div>

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