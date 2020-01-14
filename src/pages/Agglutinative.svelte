<script>
import { onMount } from "svelte";
export let syllableBank
export let mary
export let john

const test = makeBoundMorpheme(syllableBank)
const freeMorphemeTest = makeFreeMorpheme(syllableBank)


function makeBoundMorpheme(syllables){
    const morpheme = syllables[Math.floor(Math.random() * syllables.length)]
    return morpheme
}

function makeFreeMorpheme(syllables){
    //want 2-4 syllables so 1-3, and then add one?
    const syllableAmount = Math.floor(Math.random() * 3) + 1
    const randomWordSyllables =[]
    var i;
    for(i = 0; i < syllableAmount; i ++){
        randomWordSyllables.push(syllables[Math.floor(Math.random() * syllables.length)])
    }
    console.log(randomWordSyllables)
    const joinedRandomWord = randomWordSyllables.join("")
    return joinedRandomWord
}


</script>

<h1>Agglutinative Grammar Component Test:</h1>
<h2>{mary} {john} </h2>
<h3>{freeMorphemeTest}</h3>