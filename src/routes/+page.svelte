<script lang="ts">

	import { onMount } from 'svelte';
	import type { PokemonType, PokemonListType } from '../model/Pokemon'
	import Button from '$lib/components/ui/button.svelte';
	import PokemonList from '$lib/components/pokemonList.svelte';
  
	let pokemonList: PokemonListType;
	let pokemonDetails: PokemonType[]  = [];

	let currentOffset: number = 0
	let currentLimit: number = 20

	const fetchPokemonList = async(offset: number, limit: number) => {
		const response = await fetch('https://pokeapi.co/api/v2/pokemon?offset='+offset.toString()+'&limit='+limit.toString())
		if(offset === 0){
			pokemonList = await response.json();
		}
		if(offset > 0){
			const data = await response.json();
			pokemonList.results = [...pokemonList.results, ...data.results];
		}
		await fetchPokemonDetails();
	}

	const loadMorePokemon = async () => {
		currentOffset = currentOffset+20
		currentLimit = currentLimit+20
		fetchPokemonList(currentOffset, currentLimit)
		fetchPokemonDetails()
	}
  
	async function fetchPokemonDetails() {
		let theLastsPokemons = pokemonList.results.slice(- currentLimit)
		for (const pokemon of theLastsPokemons) {
			// console.log("Name : "+ pokemon.name)
			// console.log("URL : "+pokemon.url)
			const response = await fetch(pokemon.url);
			const details = await response.json();
			const sprites = details.sprites.front_default;
			//console.log("Response : "+sprites)
			pokemonDetails = [...pokemonDetails, sprites];
			//console.log("Pokemon details : "+pokemonDetails)
		}
	}

	const test = async () => {
		console.log(pokemonList)

		//console.log(pokemonDetails[0])
	}
  
	onMount(async () => {
		fetchPokemonList(currentOffset, currentLimit)
	});
	let pokemonName = '';

     function handleSubmit(event: any) {
      event.preventDefault();
      if (pokemonName.trim() !== '') {
        window.location.href = `https://pokeapi.co/api/v2/pokemon/${pokemonName.toLowerCase()}`;
      }
	  }
</script>
  

<svelte:head>
	<title>Find your pokemon</title>
	<meta name="description" content="Svelte demo app" />

</svelte:head>

<section>
	<button on:click={test}>Test</button>
	<h1>
		Find your pokemon
	</h1>
	  <input
	  type="text"
	  placeholder="Rechercher un Pokémon dans le pokedex..."
	  bind:value={pokemonName}
	  required
	/>
	<a href="/details/{pokemonName}">go to Pokedex</a> 
</section>

<section id="pokemonList">
	<h1>
		Liste Pokémons
	</h1>
	<PokemonList PokemonListProps={pokemonList} PokemonDetailsProps={pokemonDetails}/>
	{#if pokemonList && pokemonDetails.length > 0}
		<Button textProps="Charger plus de pokémons" fonctionProps={loadMorePokemon}/>
	{/if}

</section>
	  
	 

<style>

	h1{
		color: #333333;
	}
	
  /* Ajoute le style apres*/
  /* .search-bar {
    display: flex;
    align-items: center;
    gap: 10px;
  } */
 </style>
