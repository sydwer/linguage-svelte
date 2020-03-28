<script>
    import { onMount } from "svelte";
    import Select from 'svelte-select';
    import Loading from '../layout/Loading.svelte'
    import PhonemeBox from './PhonemeBox.svelte';
    import Grammar from './Grammar.svelte';
   

	const items = [
        {value: 'Arabic', 
        label: '🇪🇬 Arabic', 
        group: 'Afro-asiatic'
        },
        {value: 'English', 
        label: '🇬🇧 English', 
        group: 'European'
        },
        {value: 'German', 
        label: '🇩🇪 German', 
        group: 'European'
        },
        {value: 'Hawaiian',
        label: '🇺🇲 Hawaiian', 
        group: 'Polynesian'
        },
        {value: 'Japanese',
        label: '🇯🇵 Japanese', 
        group: 'Asian'
        },
        {value: 'Korean', 
        label: '🇰🇷 Korean', 
        group: 'Asian'
        },
        {value: 'Mandarin', 
        label: '🇨🇳 Mandarin', 
        group: 'Asian'
        },
        {value: 'Navajo', 
        label: '🇺🇸 Navajo', 
        group: 'Native American'
        },
        {value: 'Spanish', 
        label: '🇪🇸 Spanish', 
        group: 'European'
        },
        {value: 'Swahili', 
        label: '🇹🇿 Swahili', 
        group: 'African'
        },
	];
    const groupBy = (item) => item.group;
    
    let languages = undefined;
    let phonologyOrigin = undefined;
    let grammarOrigin = undefined;
    let phonemes = undefined;
    let syllableStructure = undefined;
    let syllableBank = [];
    let grammar = undefined;

    let consonants = undefined;
    let vowels = undefined;
	
	let selectedValue = undefined;
    let selectedGrammar = undefined;
    let selectedPhonology = undefined;
    let selectedLanguages = false;

    


    onMount(async function() {
        const response = await fetch("http://127.0.0.1:3000/languages");
        const json = await response.json();
        languages = json;
    });

    function resetAllVariables(){
        phonologyOrigin = undefined;
        grammarOrigin = undefined;
        phonemes = undefined;
        syllableStructure = undefined;
        grammar = undefined;
        consonants = undefined;
        vowels = undefined;
        selectedValue = undefined;
        selectedGrammar = undefined;
        selectedPhonology = undefined;
        syllableBank = [];
        selectedLanguages = false;
    };
       //Refactor this ^ when you have time

    function pullLanguageTraits(){
         phonologyOrigin = languages.find(obj=>obj.name===selectedPhonology.value);
         grammarOrigin = languages.find(obj=>obj.name===selectedGrammar.value);
         phonemes = phonologyOrigin.phonemes;
         syllableStructure = phonologyOrigin.syllable_structure.split("");
         selectedLanguages = true;
         sortPhonemes();
         makeSyllableBank();
    }

    function sortPhonemes(){
          consonants = phonemes.filter(function(phoneme) {
            return phoneme.category === "consonant";
         })
         vowels = phonemes.filter(function(phoneme) {
            return phoneme.category === "vowel";
         })
    }

    function makeSyllableBank(){
        const sonorants = makeSonorantList();
        if(phonologyOrigin.syllable_structure_2){
            if (phonologyOrigin.syllable_structure_2 === "ccv"){
                makeConsonantCluster(sonorants,25);
                var j;
                for (j = 0; j < 80; j++) {
                    generateRandomSyllable(syllableStructure)
                }
            }else{
                var i;
                for (i = 0; i < 40; i++) {
                    generateRandomSyllable(phonologyOrigin.syllable_structure_2)
                }
                var j;
                for (j = 0; j < 80; j++) {
                    generateRandomSyllable(syllableStructure)
                }
            }
        }else{
            var i;
            for (i = 0; i < 120; i++){
                generateRandomSyllable(syllableStructure)
            }
        }
        // console.log(syllableBank)
    }

    function filterPhonemes(filterValue,filterKey){
        let object = undefined
        if(filterKey === "latin"){
            object = phonemes.filter(function(phoneme) {
            return phoneme.latin === filterValue;
         })
        }else{ 
            object = phonemes.filter(function(phoneme) {
               return phoneme.manner === filterValue;
            })
        }
         return object
    };

    function filterPlosives(plosives){
        const noAlveolars = plosives.filter(function(plosive) {
               return plosive.place !== "alveolar";
            })
        const noGlottalorAlveolars = noAlveolars.filter(function(plosive) {
               return plosive.place !== "glottal";
            })
        return noGlottalorAlveolars
        
    }
    function makeSonorantList(){
        const w = phonemes.find(obj => obj.symbol === 'w');
        // const nasals = filterPhonemes("nasal", "manner");
        const laterals = filterPhonemes("lateral approximant", "manner");
        if(w){
            laterals.push(w)
            // ensuring that if w isn't in sound inventory, im not pushing an undefined item into soundBank
        }
        const rhotics = filterPhonemes("r", "latin");
        // const sonorants = nasals.concat(laterals, rhotics)
        const sonorants = laterals.concat(rhotics)
        return sonorants
    };

    function getRandomItem(array){
        const object = array[Math.floor(Math.random()*array.length)];
        return object
    }

    // CHANGE THIS TO DIFFERENT FUNCTIONS FOR EACH TYPE OF CLUSTER
    function makeConsonantCluster(sonorants,numberOfSyllables){
        const consonantClusterSyllables = [];
        const nasals = filterPhonemes("nasal", "manner");
        const allSonorants = sonorants.concat(nasals);
        const s = filterPhonemes("s", "latin").concat(filterPhonemes("sh", "latin"));
        const allPlosives = filterPhonemes("plosive", "manner");
        const plosives = filterPlosives(allPlosives);
        const startingSounds = s.concat(plosives);
        const laterals = filterPhonemes("lateral approximant", "manner");
        var i;
        for(i = 0; i < numberOfSyllables; i ++){
            const startingSound = getRandomItem(startingSounds);
            const sonorant = getRandomItem(sonorants);
            const sonorantWithN = getRandomItem(allSonorants);
            const vowel1 = getRandomItem(vowels);
            const plosive = getRandomItem(plosives);
            const lateral = getRandomItem(laterals);
            const vowel2 = getRandomItem(vowels);
            const vowel3 = getRandomItem(vowels);
            //Without these constants, the IPA doesn't match the latin, since it just re-assigns the phoneme
            const consonantCluster1IPA = [startingSound.symbol, sonorant.symbol, vowel1.symbol].join("");
            const consonantCluster1Latin = [startingSound.latin, sonorant.latin, vowel1.latin].join("");
            const consonantCluster2IPA = [plosive.symbol,lateral.symbol, vowel2.symbol].join("");
            const consonantCluster2Latin = [plosive.latin,lateral.latin, vowel2.latin].join("");
            const consonantCluster3IPA = [s.symbol,lateral.symbol, sonorantWithN.symbol, vowel3.symbol].join("");
            const consonantCluster3Latin = [s.latin,lateral.latin, sonorantWithN.latin, vowel3.latin].join("");
            const consonantCluster1 = {IPA: consonantCluster1IPA, latin: consonantCluster1Latin};
            const consonantCluster2 = {IPA: consonantCluster2IPA, latin: consonantCluster2Latin};
            const consonantCluster3 = {IPA: consonantCluster3IPA, latin: consonantCluster3Latin};
            syllableBank.push(consonantCluster1, consonantCluster2, consonantCluster3)
        }
    }

    function generateRandomSyllable(syllableForm){
        var i;
        const randomIPA = []
        const randomLatin = []
        const randomSyllableArray = []
        for (i = 0; i < syllableForm.length; i++){
            if (syllableForm[i] === "c"){
                const randomConsonant = getRandomItem(consonants);
                randomIPA.push(randomConsonant.symbol);
                randomLatin.push(randomConsonant.latin)
            }else if(syllableForm[i] === "v"){
                const randomVowel = getRandomItem(vowels);
                randomIPA.push(randomVowel.symbol);
                randomLatin.push(randomVowel.latin);
            }else if(syllableForm[i] === "n"){
                randomIPA.push("n")
                randomLatin.push("n")
            }
            else if(syllableForm[i] === "l"){
                randomIPA.push(randomIPA[1])
                randomLatin.push(randomLatin[1])
            }
            else{
                const randomPhoneme = getRandomItem(phonemes);
                randomIPA.push(randomPhoneme.symbol)
                randomLatin.push(randomPhoneme.latin)
            }
            const chance = Math.floor(Math.random() * 2)
            if(phonologyOrigin === "German" || phonologyOrigin === "English"){
                if(chance === 2){

                    const randomEnding = getRandomItem(consonants);
                randomIPA.push(randomEnding.symbol)
                randomLatin.push(randomEnding.latin)
                }
            }
        }
            const joinedRandomIPA = randomIPA.join("")
            const joinedRandomLatin = randomLatin.join("")
            const syllable = {IPA: joinedRandomIPA, latin: joinedRandomLatin}
            syllableBank.push(syllable)
    };
</script>


<style>
@import url('https://fonts.googleapis.com/css?family=Solway|Sulphur+Point&display=swap');
    /* *{font-family: 'Solway', serif;} */
    *{
        font-family: 'Solway', serif;
    }
    h1{
        padding-left: 1rem;
        text-decoration: underline;
    }

    #main{
        display: flex;
        flex-direction: row;
        justify-content: space-around;
    }
   
    #form-box{
        margin-bottom: 1rem;
        /* padding-left: 5.2rem; */
        font-family: 'Solway', serif;
        width: 25%;
    }
    #form-box>h2{
        margin-bottom: 0;
    }
    .submit-button{
        padding: 0;
        font-weight: bold;
        position: relative;
        width: 45%;
        height: 2.3rem;
        background-color: #fbfbfb2e;
        border-radius: 15px;
        border: 1px solid #293801;
        font-size: 1rem;
    }
    .submit-button:hover{
        padding: 0;
        text-decoration: none;
        border-radius: 15px;
        background-color: #749e02;
        color: white;
    }

    .yes-no-buttons{
        border-radius: 15px;
        width: 33%;
        height: 2.5rem;
        font-size: 1rem;
        font-weight: bold;
        transition: width 1s ease, color 0.4s ease 0.2s, background 0.4s ease 0.2s;
    } 

    .yes-no-buttons:hover{
        color:white;
        width: 60%;

    }
    #yes-button{
        margin-top: 0.5rem;
        border: 1px solid #293801; 
        background-color: #86ba3247;
        /* transition: width 1s ease, color 0.4s ease 0.2s, background 0.4s ease 0.2s; */
    }
    .button-box{
        display: flex;
        flex-direction: row;
    }
    #yes-box:hover > #yes-button{
        background-color: #749e02;
    }
    #yes-box:hover > #yes-arrow{
        transform: rotate(720deg);
        width: 8%;
    }
    #no-button{
        border: 1px solid #ca4646fc;
        background-color: #ca464638;
    }
    #no-box:hover > #no-button{
        background-color: #ca4646fc;
    }

    #no-box:hover > #no-arrow{
        transform: rotate(720deg);
        width: 8%;
    }
   
    img{
        align-self: center;
        width: 0;
        transition: all 0.5s ease-in-out 0s;
        margin-right: 1rem;
    }
    #custom-language-box{
        padding: 2rem;
        display: flex;
        flex-direction: row;
        /* margin-top: 2rem; */
        justify-content: space-between;
    }
    #correct-message{
        font-size: 1.25rem;
    }
     #reset-button{
        margin-top: 1rem;
        margin-left: 1rem;
        font-weight: bold;
        width: 15%;
        height: 2.3rem;
        background-color: #ca464638;
        border-radius: 15px;
        border:1px solid #ca4646fc;
        font-size: 1rem;
    }
    #reset-button:hover{
        background-color: #ca4646fc;
        color: white;
    }
    #sounds-box{
        padding:1rem;
        width: 30%;
        display: flex;
        flex-direction: column;
    }
    #sounds-box > h1{
        margin-top:0;
        font-weight: bolder;
        /* text-decoration: underline;
        text-decoration-color: #598502;  */
        color: #598502;
        text-decoration: underline;
        display: flex;
        justify-content:center;
    }
    #grammar-box{
        width:70%;
        /* display: flex; */
        /* justify-content: space-around; */
    }
    #loading-container{
        display: flex;
        align-items: center;
        justify-content: center;
    }
    p>span{
        font-weight: bold;
        text-decoration: underline;
    }
    ul>li>span{
        color:#598502;
    }
    #how-to-header{
        color:#598502;
        text-decoration: underline;
        margin: 0;
    }
    #how-to-box{
        padding: 10px;
        border: 2px double grey;
        border-radius: 7px;
    }
    .selected-language-name{
        color:#598502;
    }
</style>


{#if !selectedLanguages}
<h1>Create:</h1>
{/if}
{#if selectedLanguages}
<button id="reset-button" on:click={()=>{resetAllVariables()}}>⬅ Make A New Language</button>
{/if}
<div id = "main">
{#if !selectedLanguages}
    <div id = "form-box">
    {#if !selectedGrammar}
        <h2>Select Your Language's Traits:</h2>
        <br>
    {/if}
        {#if !selectedPhonology}
        <h3>It Should Sound like:</h3>
        <Select {items} {groupBy} bind:selectedValue></Select>
        <br>
        <button class="submit-button" on:click={() =>{
                    selectedPhonology = selectedValue;
                    selectedValue = undefined;
                    }}
                >Pick Sounds</button>
            {/if}
            {#if selectedPhonology && !selectedGrammar}
                <h3>It Will Sound Like <span class ="selected-language-name">{selectedPhonology.value}</span>,</h3>
                <h3>With the Grammar of:</h3>
                <Select {items} {groupBy} bind:selectedValue></Select>
                <br>
                <button class="submit-button" on:click={() =>{
                    selectedGrammar = selectedValue
                    }}
                >Pick Grammar</button>
            {/if}
        {#if selectedGrammar && !selectedLanguages}
        <div>
        <h2> Your language will sound like <span class = "selected-language-name">{selectedPhonology.value}</span> with 
            <span class ="selected-language-name">{selectedGrammar.value}</span> grammar.</h2>
        <h4 id ="correct-message">Is This Correct?</h4>
            <div id= "yes-box">
                <img id= "yes-arrow" src="./media/check-mark.png" alt = "arrow">
                <button class = "yes-no-buttons" id="yes-button"  on:click={()=>{
                    pullLanguageTraits()
                    }}
                >Yes</button>
            </div>
            <br>
            <div id= "no-box" class="button-box">
                <img id = "no-arrow" src="./media/x-mark.png" alt = "arrow">
                <button class = "yes-no-buttons" id="no-button"  on:click={() =>{
                    resetAllVariables()}}
                >No</button>
            </div>
        </div>
        {/if}
    </div>
         {#if !phonemes}
         <div id="loading-container">
            <Loading message = "Awaiting User Input"/>
         </div>
        {/if}
    {/if}
        <!-- {#if !phonemes}
            <Loading message = "Awaiting User Input"/>
        {/if} -->
        {#if selectedLanguages}
    <div id = "custom-language-box">
        <div id="grammar-box">
            {#if grammarOrigin}
            <div>
                <Grammar grammarOrigin={grammarOrigin} syllableBank={syllableBank} mary={phonologyOrigin.mary} john={phonologyOrigin.john}/>
            </div>
            {/if}
        </div>

        {#if phonemes}
            <div id= "sounds-box">
            <h1>Sound Inventory:</h1>
                <PhonemeBox phonemes={phonemes} />
                {#if syllableStructure}
                    <h3>Syllable Structure: "{syllableStructure.join("")}"</h3>
                {/if}
                <div id="how-to-box">
                <h2 id="how-to-header">How to Use Your Generated Grammar:</h2>
                <br/>
                <p>The <span>DICTIONARY</span> on the left of the screen holds the words used in your
                sample sentences.<br/>
                The left-most word is the English definition, followed by the translation into your language.<br/>
                The parenthesis hold your word written in the International Phonetic Alphabet.
                <br/>
                <br/>
                If you want to create your own words, use the <span>SOUND INVENTORY</span> above as a guide for what
                sounds to use.
                <br/>
                <br/>
                The <span>SYLLABLE STRUCTURE</span> listed under the box is a guide for making syllables.
                Use the structure as a template, subbing in random consonants and vowels where appropriate.<br/> 
                The "c" represents a consonant, "v" is a vowel, and "?" means either is acceptable. 
                <br/>
                <br/>
                <span>PARTICLES and CASES</span> indicate a noun's role in a sentence. These are
                used as suffixes - so you just stick them onto the end of the noun. 
                <br/>
                <br/>
                <span>GENDERS and CLASSES</span> are also used as suffixes on nouns. But they can be applied to 
                adjectives and determiners ("The", "a", "an", etc.) as well. 
                <br/>These indicate the gender of
                the word(masculine, feminine, etc), or what it is (a human, a tool, a place, etc.).<br/>
                These should be combined with <span>CASES</span>, if you have them, to more clearly
                indicate what a noun is "doing" in the context of the sentence.
                </p>
                <ul>
                    <li>Nominative: The subject/one "doing" the verb of the sentence</li>
                    <li>Accusative: The object/one being DIRECTLY affected by the verb</li>
                    <li>Dative: The indirect object/one recieving the effect of the action</li>
                    <li>Genative: Shows possession</li>
                    <li>Example: Mary's<span>[Genative]</span> sister<span>[Nominative]</span> gave 
                    a<span>[Accusative]</span> fish<span>[Accusative]</span> to the<span>[Dative]</span> 
                    cat<span>[Dative].</span></li>
                </ul>
                <p>
                    <span>TENSES</span> are placed onto the end of a verb. These mark "when" or how an action was done.<br/>
                </p>
                <ul>
                    <li>Past: The action has already happened</li>
                    <li>Present/Infinitive: The action is currently happening, or happens "in general"(e.g She runs)</li>
                    <li>Future: The action has not yet happened</li>
                    <li>Imperfect: A continuous or habitual action, most often in the past(e.g She used to run)</li>
                    <li>Conditional: An action with the potential to occur(e.g She would be tired )</li>
                </ul>
                <p><span>SAMPLE SENTENCES</span> are generated examples of how to use your grammar. They were 
                chosen to show as many verb tenses and sentence constructions as possible.
                <br/>
                The first line is your generated language.
                <br/>
                The second line is the IPA transcription of your language's sentence.
                <br/>
                The third line is the linguistic gloss of your sentence. This shows a a basic translation of words,
                with the words' genders, classes, tenses, or cases marked afterward(these are the abbreviations in all caps).
                <br/>
                The last line is the basic English translation of the sentence.
                </p>
                </div>
            </div>
        {/if}
    </div>
{/if}

</div>
