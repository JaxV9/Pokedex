<script lang="ts">

	import { onMount } from 'svelte';
	import type { PokemonType, PokemonListType } from '../model/Pokemon'
  
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
	  for (const pokemon of pokemonList.results) {
		const response = await fetch(pokemon.url);
		const details = await response.json();
		const sprites = details.sprites.front_default;	
		const id = details.id;
		pokemonDetails = [...pokemonDetails, sprites];
	  }
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
	<h1>
		Find your pokemon
	</h1>
	  <input
	  type="text"
	  placeholder="Rechercher un Pokémon dans le pkedex..."
	  bind:value={pokemonName}
	  required
	/>
	<a href="/details/{pokemonName}">go to Pokedex</a> 
</section>

<section id="pokemonList">
	<h1>
		Liste Pokémons
	</h1>
	{#if pokemonList && pokemonDetails.length > 0}
		<div id="pokemonContainerList">
			{#each pokemonList.results as pokemon, index}
				<a class="linkPokemon" href="details/{pokemon.name}">
					<div class="pokemonContainer" >
						<img src={String(pokemonDetails[index])} alt={pokemon.name} />
						<h3>{pokemon.name}<h3>
					</div>
				</a>
			{/each}
		</div>
		<button on:click={loadMorePokemon}>Charger plus de pokémons</button>
	{:else}
	<p>Chargement...</p>
	{/if}



</section>
	  
	 

<style>

	h1{
		color: #333333;
	}

	#pokemonContainerList {
		display: flex;
		flex-wrap: wrap;
		width: 100%;
		margin-left: auto;
		margin-right: auto;
	}

	.pokemonContainer{
		display: flex;
		width: 100px;
		height: 125px;
		flex-direction: column;
		align-items: center;
		margin: 10px;
		padding: 20px;
		border-radius: 10px;
		background-color: #d3d1d1;
	}
	#titre {
		display: flex;
		justify-content: center;
		height: 30px;
		margin: 30px 0;
		color: white;
	}

	.linkPokemon {
		text-decoration: none;
		color: #333333;
	}
	
  /* Ajoute le style apres*/
  /* .search-bar {
    display: flex;
    align-items: center;
    gap: 10px;
  } */
 </style>
