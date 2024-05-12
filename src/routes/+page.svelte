<script lang="ts">

	import { onMount } from 'svelte';
	import type { PokemonType, PokemonListType } from '../model/Pokemon'
	import Button from '$lib/components/ui/buttons/button.svelte';
	import PokemonList from '$lib/components/pokemonList.svelte';
	import './style.css';
	import SearchBar from '$lib/components/ui/searchBar/searchBar.svelte';
	import Layout from '../layout/Layout.svelte';
  
	let pokemonList: PokemonListType;
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
	}

	const loadMorePokemon = async () => {
		currentOffset += currentLimit
		currentPage += 1
		fetchPokemonList(currentOffset)
	}

  
	onMount(async () => {
		fetchPokemonList(currentOffset)
	});
	let pokemonName = '';


	  const test = () => {
		console.log(pokemonList.results.length)
	  }

</script>
  

<svelte:head>
	<title>Pokédex</title>
	<meta name="description" content="Svelte demo app" />

</svelte:head>
<Layout>
	<section class="section">
		<h1>Find your pokemon</h1>
		<SearchBar />
	</section>

	<section class="section">
		<h1>
			Pokemons list
		</h1>
		<p class="informations">{currentNbPokemon} pokémons out of {countPokemons}</p>
		<PokemonList PokemonListProps={pokemonList}/>
		<p class="informations">{currentNbPokemon} pokémons out of {countPokemons}</p>
		<p class="informations">Page {currentPage}</p>
		{#if pokemonList}
			<Button textProps="Load more" fonctionProps={loadMorePokemon}/>
		{/if}

	</section> 
</Layout>

<style>


 </style>