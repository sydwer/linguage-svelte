<script>
    export let syllables;
    export let dictionary;

    const possesive = {original: "'s"};
    const plural = {original: "s"};
    const tenses =[{original: "Past"},{original: "Present"},
    ];
    const helperVerbs =[{original: "Future"}, {original: "Imperfect"}, {original: "Conditional"}
    ];
    const determiners = [{original: "The"}, {original: "A"},{original: "This"}, {original: "That"}
    ,]
    

    function makeGrammar(word){
        const randomSyllable = syllables[Math.floor(Math.random() * syllables.length)];
        let IPA = randomSyllable.IPA;
        let latin = randomSyllable.latin;
        if(word === possesive){
            word.IPA = "'" + IPA;
            word.latin = "'" + latin;
        }else{
            word.IPA = IPA;
            word.latin = latin;
        }
    }

    makeGrammar(possesive);
    makeGrammar(plural);
    tenses.map(makeGrammar);
    helperVerbs.map(makeGrammar);
    determiners.map(makeGrammar);
    
        const newTenses = {};
    function markWord(words, newDictionary){
        words.map(word =>{
            const newKey = word.original.toLowerCase();
            // let newWord = { [newKey]: word};
            // word = { [newKey]: word};
            // newDictionary.push(word)
            newDictionary[newKey] = word
        })
    }

    markWord(tenses,newTenses);
    console.log(tenses)
    console.log(newTenses.past)

   
    

</script>


<style>
</style>

<h1>hi</h1>