<script>
    import { onMount } from "svelte";
	import Select from 'svelte-select';
    import PhonemeBox from './PhonemeBox.svelte';
    import Agglutinative from './Agglutinative.svelte';
   

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
         console.log(grammarOrigin.morphology.name)
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
        if(phonologyOrigin.syllable_structure_2){
                 var i;
            for (i = 0; i < 4; i++) {
                generateRandomSyllable(phonologyOrigin.syllable_structure_2)
            }
                 var j;
            for (j = 0; j < 6; j++) {
                generateRandomSyllable(syllableStructure)
            }
        }else{
            var i;
            for (i = 0; i < 10; i++){
                generateRandomSyllable(syllableStructure)
            }
        }
    }

    function generateRandomSyllable(syllableForm){
        var i;
        let randomSyllableArray = []
        for (i = 0; i < syllableForm.length; i++){
            if (syllableForm[i] === "c"){
                randomSyllableArray.push(consonants[Math.floor(Math.random()*consonants.length)].symbol)
            }else if(syllableForm[i] === "v"){
                randomSyllableArray.push(vowels[Math.floor(Math.random()*vowels.length)].symbol)
            }else if(syllableForm[i] === "n"){
                randomSyllableArray.push("n")
            }else{
                randomSyllableArray.push(phonemes[Math.floor(Math.random()*phonemes.length)].symbol)
            }
        }
            const joinedRandomSyllable = randomSyllableArray.join("")
            syllableBank.push(joinedRandomSyllable)
    }
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
    }
   
    #form-box{
        margin-bottom: 1rem;
        padding-left: 5.2rem;
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
        /* transition: width 1s ease, color 0.4s ease 0.2s, background 0.4s ease 0.2s; */
    }
    .submit-button:hover{
        padding: 0;
        text-decoration: none;
        border-radius: 15px;
        /* width: 90%; */
        background-color: #749e02;
        color: white;
    }

    .yes-no-buttons{
        border-radius: 15px;
        /* margin: 1rem; */
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
        width: 75%;
        display: flex;
        flex-direction: column;
        align-items: center;
        margin-top: 2rem;
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
</style>
{#if !selectedLanguages}
<h1>Create:</h1>
{/if}
{#if selectedLanguages}
<button id="reset-button" on:click={()=>{resetAllVariables()}}>⬅ Make A New Language</button>
{/if}
<div id = "main">
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
                    selectedPhonology = selectedValue
                    }}
                >Pick Sounds</button>
            {/if}
            {#if selectedPhonology && !selectedGrammar}
                <h3>With the Grammar of:</h3>
                <Select {items} {groupBy} bind:selectedValue></Select>
                <br>
                <button class="submit-button" on:click={() =>{
                    selectedGrammar = selectedValue
                    }}
                >Pick Grammar</button>
            {/if}
        <!-- <h3>With the Grammar of:</h3>
        <Select {items} {groupBy} bind:selectedValue></Select> -->
        {#if selectedGrammar && !selectedLanguages}
        <div>
        <h2> Your language will sound like {selectedPhonology.value} with {selectedGrammar.value} grammar.</h2>
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
    <div id = "custom-language-box">
    <!-- {#if phonemes}
        <h2>Your Language</h2>
    {/if} -->
        <PhonemeBox phonemes={phonemes} syllableStructure={syllableStructure}/>
        <!-- {#if syllableStructure}
        <Agglutinative syllableBank = {syllableBank} mary = {phonologyOrigin.mary} john = {phonologyOrigin.john}/>
        {/if} -->
        {#if grammarOrigin}
        <Agglutinative syllableBank={syllableBank} mary={phonologyOrigin.mary} john={phonologyOrigin.john}/>
        {/if}
    </div>

</div>
