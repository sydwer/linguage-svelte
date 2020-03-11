<script>
    export let syllables;
    export let dictionary;

    console.log(dictionary.names.mary)
    console.log(dictionary.nouns.keys)
    // console.log(dictionary.nouns.bear.original)
    const possesive = {original: "'s"};
    const plural = {original: "s"};
    const tenses =[{original: "Past"},{original: "Present"},
    ];
    const helperVerbs =[{original: "Future"}, {original: "Imperfect"}, {original: "Conditional"}
    ];
    

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
    tenses.map()
    console.log(dictionary)

   
    

</script>


<style>
</style>

<h1>hi</h1>