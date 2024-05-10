<script lang="ts">
	import Button from "../buttons/button.svelte";

    let pokemonName: string = ""
        
</script>

<div class="searchBarContainer">
    <input type="text" placeholder="Rechercher un Pokémon dans le pokedex..." bind:value={pokemonName} required
    class="inputSearch"/>
    <a href="/details/{pokemonName}">
        <Button textProps={"Rechercher"} widthProps={"535px"}/>
    </a> 
</div>

<style>

.searchBarContainer {
    width: 500px;
    margin-left: auto;
    margin-right: auto;
    display: grid;
    grid-template-rows: 1fr 1fr;
}

.inputSearch {
    width: calc(100% - 16px);
    height: 50px;
    margin-left: auto;
    margin-right: auto;
    padding: 0 8px;
    font-size: 18px;
    border-radius: 8px;
}

</style>