<script lang="ts">

	import { onMount } from 'svelte';
	import type { PokemonType, PokemonListType } from '../model/Pokemon'
	import Button from '$lib/components/ui/buttons/button.svelte';
	import PokemonList from '$lib/components/pokemonList.svelte';
	import './style.css';
	import SearchBar from '$lib/components/ui/searchBar/searchBar.svelte';
	import Layout from '../layout/Layout.svelte';
  
	let pokemonList: PokemonListType;
	let pokemonDetails: PokemonType[]  = [];
	let countPokemons: number = 0

	let currentOffset: number = 0
	let currentLimit: number = 20
	let currentPage: number = 1
	let currentNbPokemon: number = 0

	const fetchPokemonList = async(offset: number) => {
		const response = await fetch('https://pokeapi.co/api/v2/pokemon?offset='+offset.toString()+'&limit='+currentLimit.toString())
		if(offset === 0){
			pokemonList = await response.json();
			countPokemons = pokemonList.count
			console.log(pokemonList)
			currentNbPokemon = pokemonList.results.length
		}
		if(offset > 0){
			const data = await response.json();
			pokemonList.results = [...pokemonList.results, ...data.results];
			currentNbPokemon = pokemonList.results.length
		}
		await fetchPokemonDetails();
	}

	const loadMorePokemon = async () => {
		currentOffset += currentLimit
		currentPage += 1
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
		console.log(pokemonList.results.length)
	  }

</script>
  

<svelte:head>
	<title>Find your pokemon</title>
	<meta name="description" content="Svelte demo app" />

</svelte:head>
<Layout>
	<section class="section">
		<h1>Find your pokemon</h1>
		<SearchBar />
	</section>

	<section class="section">
		<h1>
			Liste Pokémons
		</h1>
		<p class="informations">{currentNbPokemon} pokémons sur {countPokemons}</p>
		<PokemonList PokemonListProps={pokemonList} PokemonDetailsProps={pokemonDetails}/>
		<p class="informations">{currentNbPokemon} pokémons sur {countPokemons}</p>
		<p class="informations">Page {currentPage}</p>
		{#if pokemonList && pokemonDetails.length > 0}
			<Button textProps="Charger plus de pokémons" fonctionProps={loadMorePokemon}/>
		{/if}

	</section> 
</Layout>

<style>


 </style>