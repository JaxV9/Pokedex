<script lang="ts">
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
</svelte:head>

<section>
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
			/* Ajoute ke style apres*/
			.search-bar {
			  display: flex;
			  align-items: center;
			  gap: 10px;
			}
		  </style>
