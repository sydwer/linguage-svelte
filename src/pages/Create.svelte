<script>
	import Select from 'svelte-select';

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
	
	let selectedValue = undefined;
    let selectedGrammar = undefined;
    

    
</script>


<style>
@import url('https://fonts.googleapis.com/css?family=Solway|Sulphur+Point&display=swap');
    /* *{font-family: 'Solway', serif;} */
    *{
        font-family: 'Solway', serif;
    }
    h1{
        padding-left: 3rem;
    }
    #form-box{
        padding-left: 5.2rem;
        font-family: 'Solway', serif;
        width: 33%;
    }
    #submit-button{
        padding: 0;
        font-weight: bold;
        position: relative;
        /* overflow: visible; */
        /* text-decoration-line: underline; */
        margin-top: 2rem;
        width: 45%;
        height: 2.3rem;
        background-color: #89bb022e;
        border-radius: 15px;
        border: 1px solid #293801;
        font-size: 1rem;
        transition: width 1s ease, color 0.4s ease 0.2s, background 0.4s ease 0.2s;
    }
    #submit-button:hover{
        padding: 0;
        text-decoration: none;
        border-radius: 15px;
        width: 90%;
        background-color: #749e02;
        color: white;
    }
    img{
        width: 4%;
    }
</style>

<h1>Create Your Language:</h1>
<div id = "form-box">
<h2>It Should Sound like:</h2>
<Select {items} {groupBy} bind:selectedValue></Select>
<h2>With the Grammar of:</h2>
<Select {items} {groupBy} bind:selectedGrammar></Select>
<div>
<img src="./media/arrow.png" alt = "arrow">
    <button id="submit-button" on:click={() =>{
        console.log(selectedValue)}}
    >Create Language</button>
</div>
<!-- <button id="submit-button" on:click={() =>{
        console.log(selectedValue)}}
    >Create Language</button> -->
</div>
<!-- {#if selectedValue}
	<p>Selected value is: {selectedValue.label}</p>
{/if} -->
