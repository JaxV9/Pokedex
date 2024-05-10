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
                </div>
            </a>
        {/each}
    </div>
    {:else}
    <p>Chargement...</p>
    {/if}

    
    
<style>
	#pokemonContainerList {
		display: flex;
		flex-wrap: wrap;
		width: 100%;
		margin-left: auto;
		margin-right: auto;
        margin-bottom: 50px;
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
</style>