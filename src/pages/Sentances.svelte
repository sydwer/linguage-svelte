<script>
    // export let grammarOrigin;
    export let names;
    export let nouns;
    export let pronouns;
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
    const bear = findWord(nouns, "Bear");
    const ten = findWord(nouns, "Ten");
    const book = findWord(nouns, "Book");
    const hunger = findWord(nouns, "Hunger");
    const rock = findWord(nouns, "Rock");
    const river = findWord(nouns, "River");

    const big = findWord(adjectives, "Big");
    const fast = findWord(adjectives, "Fast");

    const i = findWord(pronouns, "I");
    const he = findWord(pronouns, "He");
    const we = findWord(pronouns, "We");

    const say = findWord(verbs, "Say");
    const give = findWord(verbs, "Give");
    const die = findWord(verbs, "Die");
    const eat = findWord(verbs, "Eat");
    const able = findWord(verbs, "Able To");
    const have = findWord(verbs, "Have");
    const want = findWord(verbs, "Want");

    const past = findWord(tenses, "Past");
    const present = findWord(tenses, "Present");
    const nonPast = findWord(tenses, "Non-Past");
    const future = findWord(tenses,"Future");
    const cond = findWord(tenses,"Conditional");
    const ipfv = findWord(tenses, "Imperfect");

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
    const adv = findWord(determiners, "Adverb Marker");

    
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
<br/>

<div>
{#if !present}
    <h4>{we.latin} {have.latin}{nonPast.latin} {hunger}</h4>
    <h4>{we.IPA} {have.IPA}{nonPast.IPA} {hunger}</h4>
    {:else}
    <h4>{we.latin} {have.latin}{present.latin} {hunger}</h4>
    <h4>{we.IPA} {have.IPA}{present.IPA} {hunger}</h4>
    {/if}
    <h4>1PL have.PRES hunger</h4>
    <h4> 'We're hungry.'</h4>
</div>

<div>
    <h4>{i.latin} {give.latin}{ipfv.latin} {book.latin} {a.latin}{gen.latin} {i.latin} {he.latin}{dat.latin} </h4>
    <h4>{i.IPA} {give.IPA}{ipfv.IPA} {book.IPA} {a.IPA}{gen.IPA} {i.IPA} {he.IPA}{dat.IPA} </h4>
    <h4>1SG.NOM give.COND book DET.GEN 1SG 3SG/MASC.DAT</h4>
    <h4>'I would give him my book.'</h4>
</div>
<br/>

<div>
    <h4>{i.latin} {want.latin}{past.latin} {a.latin}{dat.latin} {rock.latin}{dat.latin} {a.latin}{gen.latin} {river.latin}{gen.latin}</h4>
    <h4>{i.IPA} {want.IPA}{past.IPA} {a.IPA}{dat.IPA} {rock.IPA}{dat.IPA} {a.IPA}{gen.IPA} {river.IPA}{gen.IPA}</h4>
    <h4>1SG want.PAST DET.DAT rock.DAT DET.GEN river.GEN</h4>
    <h4>'I wanted a rock from the river.'</h4>
</div>

<div>
{#if !present}
    <h4>{a.latin}{nom.latin} {bear.latin}{nom.latin} {big.latin}{nom.latin} {able.latin}{cond.latin}
        {ten.latin} {fish.latin}{acc.latin}{pl.latin} {fast.latin}{adv.latin} {eat.latin}{nonPast.latin}</h4>
    <h4>{a.IPA}{nom.IPA} {bear.IPA}{nom.IPA} {big.IPA}{nom.IPA} {able.IPA}{cond.IPA}
        {ten.IPA} {fish.IPA}{acc.IPA}{pl.IPA} {fast.IPA}{adv.IPA} {eat.IPA}{nonPast.IPA}</h4>
    {:else}
         <h4>{a.latin}{nom.latin} {bear.latin}{nom.latin} {big.latin}{nom.latin} {able.latin}{cond.latin}
        {ten.latin} {fish.latin}{acc.latin}{pl.latin} {fast.latin}{adv.latin} {eat.latin}{present.latin}</h4>
    <h4>{a.IPA}{nom.IPA} {bear.IPA}{nom.IPA} {big.IPA}{nom.IPA} {able.IPA}{cond.IPA}
        {ten.IPA} {fish.IPA}{acc.IPA}{pl.IPA} {fast.IPA}{adv.IPA} {eat.IPA}{present.IPA}</h4>
    {/if}
    <h4>DET.NOM bear.NOM big.NOM able.COND ten fish.ACC.PL fast.ADV eat.INF</h4>
    <h4>'A big bear could eat 10 fish quickly.'</h4>
</div>