<script lang="ts">

	import { onMount } from 'svelte';

	let pokemonList;

	onMount(async () => {
		const response = await fetch('https://pokeapi.co/api/v2/pokemon?limit=151');
		pokemonList = await response.json();
		console.log(pokemonList.results)
		// const response = await fetch(pokemonList.url);
		// pokemonImage = await response.json();
		// console.log(pokemonImage)
	});

</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<h1>
		Hello
	</h1>
</section>

<section id="pokemonList">
	{#if pokemonList}
	<div class="pokemonContainer">
		{#each pokemonList.results as pokemon}
			<div>
				<h2>
					{pokemon.name}
				</h2>
			</div>
			<div>
				<img src={pokemon.sprites} alt={pokemon.name}>
			</div>
		{/each}
	</div>
	{:else}
	<p>Chargement...</p>
	{/if}

</section>

<style>
	*{
		margin: 0;
		padding: 0;
	}

	s-y_bCXRrkrYfP{
		display: flex;
	}
</style>
