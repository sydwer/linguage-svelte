<script>
    // export let grammarOrigin;
    export let names;
    export let nouns;
    export let verbs;
    export let adjectives;
    export let tenses;
    export let genders;
    export let cases;
    export let determiners;
    
    function findWord(array, latinValue){
        const obj = array.find(obj => obj.original === latinValue)
        return obj
    }
    const mary = names.find(obj => obj.latin === 'Mary');
    const john = names.find(obj => obj.latin === 'John');
    const hello = findWord(nouns,"Hello");
    const cat = findWord(nouns, "Fish");
    const fish = findWord(nouns, "Cat");
    const tree = findWord(nouns, "Tree");

    const say = findWord(verbs, "Say");
    const give = findWord(verbs, "Give");
    const die = findWord(verbs, "Die");
    const eat = findWord(verbs, "Eat");

    const past = findWord(tenses, "Past");
    const present = findWord(tenses, "Present");
    const nonPast = findWord(tenses, "Non-Past");
    const future = findWord(tenses,"Future");

    const nom = findWord(cases,"Nominative");
    const acc = findWord(cases, "Accusative");
    const dat = findWord(cases, "Dative");
    const gen = findWord(cases, "Genative");

    const masc = findWord(genders, "Masculine");
    const fem = findWord(genders, "Feminine");
    const nuet = findWord(genders, "Neutral");
    const pl = findWord(genders, "Plural");

    const a = findWord(determiners, "A");
    const the = findWord(determiners, "The");

    
</script>

<style>

h4{
    margin-bottom: 0;
}
div{
    display: flex;
    flex-direction: column;
    align-items: center;
    border-bottom: 1px solid grey;
}

</style>

<div>
{#if !present}
    <h4>{mary.latin}{nom.latin} {say.latin}{nonPast.latin}, "{hello.latin}".</h4>
    <h4>{mary.IPA}{nom.IPA} {say.IPA}{nonPast.IPA} "{hello.IPA}"</h4>
{:else}
    <h4>{mary.latin}{nom.latin} {say.latin}{present.latin}, "{hello.latin}".</h4>
    <h4>{mary.IPA}{nom.IPA} {say.IPA}{present.IPA} "{hello.IPA}"</h4>
{/if}
    <h4> Mary.NOM say.PRES Hello</h4>
    <h4>'Mary says, "Hello".'</h4>
</div>
<br/>

<div>
    <h4>{the.latin}{nom.latin} {tree.latin}{nom.latin} {die.latin}{past.latin}</h4>
    <h4>{the.IPA}{nom.IPA} {tree.IPA}{nom.IPA} {die.IPA}{past.IPA}</h4>
    <h4>DET.NOM tree.NOM die.PST</h4>
    <h4>'The tree died.'</h4>
</div>
<br/>
<div>
{#if !future}
    <h4>{the.latin}{nom.latin} {cat.latin}{nom.latin}{pl.latin} {eat.latin}{nonPast.latin} {fish.latin}{acc.latin}</h4>
    <h4>{the.IPA}{nom.IPA} {cat.IPA}{nom.IPA}{pl.IPA} {eat.IPA}{nonPast.IPA} {fish.IPA}{acc.IPA}</h4>
{:else}
    <h4>{the.latin}{nom.latin} {cat.latin}{nom.latin}{pl.latin} {eat.latin}{future.latin} {fish.latin}{acc.latin}</h4>
    <h4>{the.IPA}{nom.IPA} {cat.IPA}{nom.IPA}{pl.IPA} {eat.IPA}{future.IPA} {fish.IPA}{acc.IPA}</h4>
    {/if}
    <h4>DET.NOM cat.NOM.PL eat.FUT fish.ACC</h4>
    <h4>'The cats will eat fish.'</h4>
</div>