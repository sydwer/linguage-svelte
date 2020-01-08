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
        group: 'Eropean'
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
    
	let selectedValue = undefined;
    let selectedGrammar = undefined;
    

    
</script>

<h1>Create A Language</h1>

<h2>What Language's Sound System Do You Like?</h2>
<Select {items} bind:selectedValue></Select>
<h2>What Language's Grammar System Do You Like?</h2>
<Select {items} bind:selectedGrammar></Select>
<button on:click={() =>{
        console.log(selectedValue)}}
    >Submit</button>

{#if selectedValue}
	<p>Selected valued is: {selectedValue.label}</p>
{/if}
