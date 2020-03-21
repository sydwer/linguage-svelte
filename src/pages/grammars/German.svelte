<script>
// export let syllables;
export let dictionary;
export let makeGrammar;
export let markWord;


const names = dictionary.names;
const nouns = dictionary.nouns;
const pronouns = dictionary.pronouns;
const verbs = dictionary.verbs;
const adjectives = dictionary.adjectives;

// There's a ton of cases markers in German, see if you can't rework this to be more concise
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

const cases = [mascDet, femDet, neutDet, plDet, mascArt, femArt, neutArt, plArt, 
nomEndings, accEndings, datEndings, genEndings];
// Det is determiners('the'), and Art is articles('a' or 'an')

const prepositions = [{original: "By"}, {original: "Through"}, {original: "Along"}, {original: "For"}, {original: "Against"},
{original: "Towards"}, {original: "Without"},{original: "About"},];

function makeGrammarDictionaries(){
  prepositions.map(makeGrammar);
  cases.map(caseType => {
    caseType.map(makeGrammar)
  })
}

function makeKeys(){
  markWord(prepositions);
  cases.map(caseType => {
    markWord(caseType)
  })
}

function makeGermanGrammar(){
  makeGrammarDictionaries();
  makeKeys();
}

makeGermanGrammar();




  // mascDet.map(makeGrammar)
  // femDet.map(makeGrammar)
  // neutDet.map(makeGrammar)
  // plDet.map(makeGrammar)
  // mascArt.map(makeGrammar)
  // femArt.map(makeGrammar)
  // neutArt.map(makeGrammar)
  // plArt.map(makeGrammar)




// console.log(test)


</script>



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