<script script="ts">

	import { onMount } from 'svelte';
  
	let pokemonList;
	let pokemonDetails = [];
  
	async function fetchPokemonDetails() {
	  for (const pokemon of pokemonList.results) {
		const response = await fetch(pokemon.url);
		const details = await response.json();
		const sprites = details.sprites.front_default;	
		console.log(pokemonList)
		pokemonDetails = [...pokemonDetails, sprites];
	  }
	}
  
	onMount(async () => {
	  const response = await fetch('https://pokeapi.co/api/v2/pokemon?limit=151');
	  pokemonList = await response.json();
	  await fetchPokemonDetails();
	});

</script>
  

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<h1>
		Liste Pokemon
	</h1>
</section>

<section id="pokemonList">
	{#if pokemonList && pokemonDetails.length > 0}
		<ul>
			{#each pokemonList.results as pokemon, index}
			<li>
				<img src={pokemonDetails[index]} alt={pokemon.name} />
				{pokemon.name}
			</li>
			{/each}
		</ul>
	{:else}
	<p>Chargement...</p>
	{/if}
</section>

<style>
	*{
		margin: 0;
		padding: 0;
	}
</style>
