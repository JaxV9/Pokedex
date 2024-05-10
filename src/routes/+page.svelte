<script script="ts">

	import { onMount } from 'svelte';
  
	let pokemonList;
	let pokemonDetails = [];
  
	async function fetchPokemonDetails() {
	  for (const pokemon of pokemonList.results) {
		const response = await fetch(pokemon.url);
		const details = await response.json();
		const sprites = details.sprites.front_default;	
		const id = details.id;
		// console.log(id)
		// console.log(pokemonList)
		pokemonDetails = [...pokemonDetails, sprites];
		// console.log(id)
	  }
	}
  
	onMount(async () => {
	  const response = await fetch('https://pokeapi.co/api/v2/pokemon?limit=151');
	  pokemonList = await response.json();
	  await fetchPokemonDetails();
	});
	let pokemonName = '';
	  
     // Fonction pour gérer le form normalement
     function handleSubmit(event) {
      event.preventDefault();
      if (pokemonName.trim() !== '') {
        // ouvre la page du Pokémon
        window.location.href = `https://pokeapi.co/api/v2/pokemon/${pokemonName.toLowerCase()}`;
      }
	  }
</script>
  

<svelte:head>
	<title>Find your pokemon</title>
	<meta name="description" content="Svelte demo app" />
	<link rel="preconnect" href="https://fonts.googleapis.com">
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
	<link href="https://fonts.googleapis.com/css2?family=Kanit:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&family=Open+Sans:ital,wght@0,300..800;1,300..800&family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap" rel="stylesheet">
</svelte:head>

<section id="titre">
	<h1>
		Liste Pokemon
	</h1>
</section>

<section id="pokemonList">
	{#if pokemonList && pokemonDetails.length > 0}
		<div id="pokemonContainerList">
			{#each pokemonList.results as pokemon, index}
				<a class="linkPokemon" href="/{pokemon.name}">
					<div class="pokemonContainer" >
						<img src={pokemonDetails[index]} alt={pokemon.name} />
						<h3>{pokemon.name}<h3>
					</div>
				</a>
			{/each}
		</div>
	{:else}
	<p>Chargement...</p>
	{/if}
	<h1>
		Find your pokemon
	</h1>
</section>
	  
	 
	  
	  <!-- bouton pour chercher -->
		<input
		  type="text"
		  placeholder="Rechercher un Pokémon dans le pkedex..."
		  bind:value={pokemonName}
		  required
		/>
		<a href="/details/{pokemonName}">go to Pokedex</a> 


<style>
	@import "style.css";

	h1{
		color: #333333;
	}

	#pokemonContainerList {
		display: flex;
		justify-content: space-between;
		height: calc(100vh - 100px);
		overflow: auto;
		flex-wrap: wrap;
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
	
  /* Ajoute ke style apres*/
  .search-bar {
    display: flex;
    align-items: center;
    gap: 10px;
  }
 </style>
