<script lang="ts">
    
    /** @type {import('./$types').PageData} */
    /** @type {import('./$types').PageLoad} */
    import { page } from '$app/stores';
	import { onMount } from 'svelte';
	import Layout from '../../../layout/Layout.svelte';
    import '../../style.css';
    import { error, redirect } from '@sveltejs/kit';
    import { goto } from '$app/navigation';
    
    let pokemonData: any = null;
    
    const fetchData = async () => {
        const response = await fetch("https://pokeapi.co/api/v2/pokemon/" + $page.params.slug);
        if(response){
            const data = await response.json();
            pokemonData = data;
        }
        if(!response.ok){
            goto('/404');
        }
    }
    onMount(fetchData);

    const test = () => {
        console.log(pokemonData.types)
    }
</script>
    <Layout>
        {#if pokemonData !== null}
        <section class="pokemonSection">
            <h1>{pokemonData.name}</h1>
        <div class="pokemonDatasContainer">
            <div class="pokemonPictureContainer">
                
                <img class="pokemonPicture" src={"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/"+pokemonData.id+".png"} alt={pokemonData.name}/>
            </div>
            <div class="pokemonStatsContainer">
                <div class="stats">
                    <span class="pokemonStatsTitle">Taille :</span>
                    <span class="pokemonStatsValue">{pokemonData.height/10} m</span>
                </div>
                <div class="stats">
                    <span class="pokemonStatsTitle">Poids :</span>
                    <span class="pokemonStatsValue">{pokemonData.weight/10} kg</span>
                </div>
                <div class="stats">
                    <span class="pokemonStatsTitle">Types :</span>
                    {#each pokemonData.types as types}
                        <span class="pokemonStatsValue">{types.type.name}</span>
                    {/each}
                </div>
                <div class="stats">
                    <span class="pokemonStatsTitle">Abilities :</span>
                    {#each pokemonData.abilities as abilities}
                        <span class="pokemonStatsValue">{abilities.ability.name}</span>
                    {/each}
                </div>
            </div>
        </div>
    </section>

        {:else}
            <p>Loading...</p>
        {/if}
    </Layout>


<style>

    .pokemonSection {
        margin-top: 50px;
        padding-bottom: 50px;
        width: 70%;
        margin-left: auto;
        margin-right: auto;
    }

    .pokemonSection > h1 {
        text-align: center;
        margin-top: 0;
        margin-bottom: 28px;
        text-transform: capitalize;
        font-size: 35px;

    }

    .pokemonPictureContainer {
        border-radius: 16px;
        padding: 16px;

    }

    .pokemonPicture {
        width: 100%;
        max-width: 400px;
    }

    .pokemonDatasContainer {
        width: 100%;
        display: grid;
        grid-template-columns: 1fr 1fr;
    }

    .pokemonStatsContainer {
        width: 100%;
        height: fit-content;
        margin-left: auto;
        margin-right: auto;
        display: flex;
        font-size: 18px;
        background-color: #30A7D7;
        padding: 16px 28px;
        border-radius: 16px;
        display: grid;
        grid-template-columns: 1fr 1fr;
        column-gap: 8px;
        row-gap: 28px;
    }

    .pokemonStatsTitle {
        display: block;
        margin-left: auto;
        margin-right: auto;
        margin-bottom: 8px;
        font-size: 18px;
        color: #333333;
        text-align: justify;
    }

    .pokemonStatsValue {
        display: block;
        margin-left: auto;
        margin-right: auto;
        margin-bottom: 8px;
        font-size: 18px;
        color: #FFFFFF;
        text-align: justify;
    }

    .stats > p {
        text-align: center;
    }



</style>