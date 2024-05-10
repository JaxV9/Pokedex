<script lang="ts">
	import Button from "../buttons/button.svelte";

    let pokemonName: string = ""
        
</script>

<div class="searchBarContainer">
    <input type="text" placeholder="Search a pokemon" bind:value={pokemonName} required
    class="inputSearch"/>
    {#if pokemonName !== ""}
        <a href="/details/{pokemonName}">
            <Button textProps={"Gotta catch em all !"} enabledProps={true} widthProps={"516px"}/>
        </a> 
        {:else}
        <Button textProps={"Gotta catch em all"} enabledProps={false} widthProps={"516px"}/>
    {/if}
    
       
    
</div>

<style>

.searchBarContainer {
    width: 500px;
    margin-left: auto;
    margin-right: auto;
}

.inputSearch {
    width: 500px;
    height: 50px;
    margin-left: auto;
    margin-right: auto;
    margin-bottom: 16px;
    padding: 0 8px;
    font-size: 18px;
    border-radius: 8px;
    border: 0px;
}

</style>