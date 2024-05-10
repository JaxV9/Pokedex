<script lang="ts">

	import { onMount } from 'svelte';
	import type { PokemonType, PokemonListType } from '../model/Pokemon'
	import Button from '$lib/components/ui/button.svelte';
	import PokemonList from '$lib/components/pokemonList.svelte';
  
	let pokemonList: PokemonListType;
	let pokemonDetails: PokemonType[]  = [];

	let currentOffset: number = 0
	let currentLimit: number = 20

	const fetchPokemonList = async(offset: number) => {
		const response = await fetch('https://pokeapi.co/api/v2/pokemon?offset='+offset.toString()+'&limit='+currentLimit.toString())
		console.log("This fetch : " + 'https://pokeapi.co/api/v2/pokemon?offset='+offset.toString()+'&limit='+currentLimit.toString())
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
		currentOffset += currentLimit
		fetchPokemonList(currentOffset)
	}
  
	async function fetchPokemonDetails() {
		let theLastsPokemons = pokemonList.results.slice(- currentLimit)
		for (const pokemon of theLastsPokemons) {
			const response = await fetch(pokemon.url);
			const details = await response.json();
			const sprites = details.sprites.front_default;
			pokemonDetails = [...pokemonDetails, sprites];
		}
		console.log(pokemonList)
	}
  
	onMount(async () => {
		fetchPokemonList(currentOffset)
	});
	let pokemonName = '';

     function handleSubmit(event: any) {
      event.preventDefault();
      if (pokemonName.trim() !== '') {
        window.location.href = `https://pokeapi.co/api/v2/pokemon/${pokemonName.toLowerCase()}`;
      }
	  }

	  const test = () => {
		console.log(pokemonDetails)
	  }


</script>
  

<svelte:head>
	<title>Find your pokemon</title>
	<meta name="description" content="Svelte demo app" />

</svelte:head>

<section>
	<button on:click={test}>test</button>
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
