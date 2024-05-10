<script lang="ts">
    export let PokemonListProps;
    export let PokemonDetailsProps;
        
</script>
        
    {#if PokemonListProps && PokemonDetailsProps.length > 0}
    <div id="pokemonContainerList">
        {#each PokemonListProps.results as pokemon, index}
            <a class="linkPokemon" href="details/{pokemon.name}">
                <div class="pokemonContainer" >
                    <img src={"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/"+[index+1]+".png"} alt=""/>
                    <h3>{pokemon.name}</h3>
					<p class="pokemonDetails"> N°{index+1}</p>
                </div>
            </a>
        {/each}
    </div>
    {:else}
    <p>Chargement...</p>
    {/if}

<style>
	#pokemonContainerList {
		display: grid;
		grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
		column-gap: 16px;
		row-gap: 16px;
		width: 100%;
		margin-left: auto;
		margin-right: auto;
        margin-bottom: 28px;
	}

	.pokemonDetails {
		font-size: 14px;
		color: #333333;
	}

	.pokemonContainer{
		display: flex;
		width: 100%;
		height: fit-content;
		flex-direction: column;
		align-items: center;
		border-radius: 10px;
		background-color: #d3d1d1;
		transition: all ease 0.2s;
	}

	.pokemonContainer:hover {
		scale: 1.1;
		transition: all ease 0.2s;
		background-color: #bababa;
	}

	.pokemonContainer > img {
		width: 150px;
	}

	.linkPokemon {
		width: fit-content;
		text-decoration: none;
		color: #333333;
	}
</style>