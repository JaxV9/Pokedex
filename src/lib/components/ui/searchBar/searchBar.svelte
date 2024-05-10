<script lang="ts">
    let pokemonName: string = ""
        
</script>
        
<input type="text" placeholder="Rechercher un Pokémon dans le pokedex..." bind:value={pokemonName} required
class="inputSearch"/>
<a href="/details/{pokemonName}">go to Pokedex</a> 
    
<style>


</style>