<script>
// import {onMount } from 'svelte'
import Dictionary from './Dictionary.svelte'
export let syllableBank;
export let mary;
export let john;


    const nounDictionary = [{original: "Apple", IPA: undefined, latin: undefined},{original: "Bear", IPA: undefined, latin: undefined},
        {original: "Book", IPA: undefined, latin: undefined}, {original: "Cat", IPA: undefined, latin: undefined}, 
        {original: "Dinner", IPA: undefined, latin: undefined}, {original: "Fish", IPA: undefined, latin: undefined},
        {original: "Hello", IPA: undefined, latin: undefined}, {original: "House", IPA: undefined, latin: undefined},
        {original: "Hunger", IPA: undefined, latin: undefined}, {original: "River", IPA: undefined, latin: undefined},
        {original: "Ten", IPA: undefined, latin: undefined}, {original: "Tree", IPA: undefined, latin: undefined},]

    const verbDictionary = [{original: "Eat", IPA: undefined, latin: undefined}, {original: "Die", IPA: undefined, latin: undefined}, 
        {original: "Give", IPA: undefined, latin: undefined}, {original: "Have", IPA: undefined, latin: undefined}, 
        {original: "Say", IPA: undefined, latin: undefined}, {original: "To Be", IPA: undefined, latin: undefined}, 
        {original: "Want", IPA: undefined, latin: undefined},
        ];

    const adjectiveDictionary = [{original: "Big", IPA: undefined, latin: undefined}, 
        {original: "Cute", IPA: undefined, latin: undefined}, {original: "Fast", IPA: undefined, latin: undefined}, 
        {original: "Hungry", IPA: undefined, latin: undefined},
        ];

    const pronounDictionary = [{original: "I", IPA: undefined, latin: undefined},{original:"You", IPA: undefined, latin: undefined},
        {original:"He", IPA: undefined, latin: undefined},{original:"She", IPA: undefined, latin: undefined},
        {original:"It", IPA: undefined, latin: undefined},{original:"We", IPA: undefined, latin: undefined},
        {original:"You (Plural)", IPA: undefined, latin: undefined},{original:"They", IPA: undefined, latin: undefined},];

    const affixes =[{original: "Present", IPA: undefined, latin: undefined},{original: "Past", IPA: undefined, latin: undefined},
        {original: "Future", IPA: undefined, latin: undefined}, {original: "Imperfect", IPA: undefined, latin: undefined},
        {original: "Conditional", IPA: undefined, latin: undefined}];

    // ^^^Sort alphabetically and by part of speech^^^// 
    if(syllableBank){
        makeDictionary(nounDictionary);
        makeDictionary(verbDictionary);
        makeDictionary(adjectiveDictionary);
        makeDictionary(pronounDictionary);
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
            if (dictionary === affixes){
                newWord = makeBoundMorpheme(syllableBank)
            }else{
                newWord = makeFreeMorpheme(syllableBank)
            }
            dictionary[i].IPA = newWord.IPA
            dictionary[i].latin = newWord.latin
        }
        console.log(affixes)
    }

</script>

<style>
    h2{
        font-weight: bolder;
    }
</style>

<!-- <h1>Agglutinative Grammar Component Test:</h1> -->
<!-- <h2>{mary} {john} </h2> -->

<h1>Dictionary</h1>
<h4>*Paranthesis indicate the IPA transcription of each word*</h4>
<Dictionary category = "Nouns" dictionary={nounDictionary}/>
<Dictionary category = "Pronouns" dictionary={pronounDictionary}/>
<Dictionary category = "Verbs" dictionary={verbDictionary}/>
<Dictionary category = "Adjectives" dictionary={adjectiveDictionary}/>


<!-- <h4>{dictionary}</h4> -->