<script>
    import { onMount } from "svelte";
	import Select from 'svelte-select';
    import SyllableList from './SyllableList.svelte'

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
    let grammar = undefined;

    let consonants = undefined;
    let vowels = undefined;
	
	let selectedValue = undefined;
    let selectedGrammar = undefined;
    let selectedPhonology = undefined;

    


    onMount(async function() {
        const response = await fetch("http://127.0.0.1:3000/languages");
        const json = await response.json();
        languages = json;
    });


    function pullLanguageTraits(){
         phonologyOrigin = languages.find(obj=>obj.name===selectedPhonology.value);
         grammarOrigin = languages.find(obj=>obj.name===selectedGrammar.value);
         phonemes = phonologyOrigin.phonemes;
         syllableStructure = phonologyOrigin.syllable_structure.split("");
         consonants = phonemes.filter(function(phoneme) {
            return phoneme.category === "consonant";
         })
         vowels = phonemes.filter(function(phoneme) {
            return phoneme.category === "vowel";
         })
         console.log(consonants)
         console.log(vowels)
    }

    // function makeSyllables(){
    //     var i;
    //     for (i = 0; i < 100; i++) {
    //         var i2;
    //         for (i2 = 0; i2< syllableStructure.length; i2++){
    //             let randomSyllable = []
    //             if (syllableStructure[i2] === "c"){
    //                 randomSyllable.push
    //             }
    //         }
    //     }
    // }

   

</script>


<style>
@import url('https://fonts.googleapis.com/css?family=Solway|Sulphur+Point&display=swap');
    /* *{font-family: 'Solway', serif;} */
    *{
        font-family: 'Solway', serif;
    }
    #main{
        display: flex;
        flex-direction: row;
    }
    h2{
        margin-bottom: 3.5rem;
    }
   
    #form-box{
        margin-top: 2rem; 
        margin-bottom: 1rem;
        padding-left: 5.2rem;
        font-family: 'Solway', serif;
        width: 25%;
    }
    #form-box>h2{
        padding-left: 1rem;
    }
    .submit-button{
        padding: 0;
        font-weight: bold;
        position: relative;
        /* overflow: visible; */
        /* text-decoration-line: underline; */
        margin-top: 2rem;
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
</style>

<div id = "main">
    <div id = "form-box">
        <h2>Select Your Language's Traits:</h2>
        {#if !selectedPhonology}
        <h3>It Should Sound like:</h3>
        <Select {items} {groupBy} bind:selectedValue></Select>
        <button class="submit-button" on:click={() =>{
                    selectedPhonology = selectedValue
                    }}
                >Pick Sounds</button>
            {/if}
            {#if selectedPhonology && !selectedGrammar}
                <h3>With the Grammar of:</h3>
                <Select {items} {groupBy} bind:selectedValue></Select>
                <button class="submit-button" on:click={() =>{
                    selectedGrammar = selectedValue
                    }}
                >Pick Grammar</button>
            {/if}
        <!-- <h3>With the Grammar of:</h3>
        <Select {items} {groupBy} bind:selectedValue></Select> -->
        {#if selectedGrammar}
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
                    selectedValue = undefined
                    selectedPhonology = undefined
                    selectedGrammar = undefined
                    }}
                >No</button>
            </div>
        </div>
        {/if}


    </div>
    <div id = "custom-language-box">
        <h2>Your Language</h2>
        <SyllableList phonemes = {phonemes} syllableStructure = {syllableStructure}/>
    </div>

</div>
