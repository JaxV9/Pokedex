<script lang="ts">
    
    /** @type {import('./$types').PageData} */
    /** @type {import('./$types').PageLoad} */
    import { page } from '$app/stores';
	import Layout from '../../../layout/Layout.svelte';
    import '../../style.css';
    let pokemonData: any = null;
    
    const fetchData = async () => {
        await fetch("https://pokeapi.co/api/v2/pokemon/" + $page.params.slug)
            .then((response: Response) => {
                //console.log(response.json());
                return response.json()
            })
            .then((data:any) => {
                console.log(data.sprites.front_shiny)
                pokemonData = data;
            })
    }
    fetchData();

    const test = () => {
        console.log(pokemonData.types)
    }
</script>
    <Layout>
        {#if pokemonData !== null}
        <section class="pokemonSection">
        <div class="pokemonDatasContainer">
            <div class="pokemonPictureContainer">
                <h1>{pokemonData.name}</h1>
                <img class="pokemonPicture" src={"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/"+pokemonData.id+".png"} alt={pokemonData.name}/>
            </div>
            <div class="pokemonStatsContainer">
                <div class="stats">
                    <p>Taille :</p>
                    <p>{pokemonData.height/10} m</p>
                </div>
                <div class="stats">
                    <p>Poids :</p>
                    <p>{pokemonData.weight/10} kg</p>
                </div>
                <div class="stats">
                    <p>Types :</p>
                    {#each pokemonData.types as types}
                        <p>{types.type.name}</p>
                    {/each}
                </div>
                <div class="stats">
                    <p>Abilities :</p>
                    {#each pokemonData.abilities as abilities}
                        <p>{abilities.ability.name}</p>
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

    .pokemonDatasContainer {
    }

    .pokemonPictureContainer {
        border-radius: 16px;
        padding: 16px;

    }

    .pokemonPictureContainer > h1 {
        text-align: center;
        margin-bottom: 0;
        text-transform: capitalize;
        font-size: 28px;
    }

    .pokemonPicture {
        width: 500px;
    }

    .pokemonDatasContainer {
        width: 100%;
        display: grid;
        grid-template-columns: 1fr 2fr;
    }

    .pokemonStatsContainer {
        width: 80%;
        height: fit-content;
        margin-left: auto;
        margin-right: auto;
        height: auto;
        display: flex;
        font-size: 20px;
        background-color: #30A7D7;
        padding: 16px;
        border-radius: 16px;
		display: grid;
		grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
		column-gap: 16px;
		row-gap: 16px;
    }

    .stats > p {
        text-align: center;
    }

    .statsContainer {
        width: 500px;
        display: grid;
        grid-template-columns: 20% 80%;
        margin-bottom: 16px;
    }

    .numberStats {
        margin-bottom: 16px;
    }

    .label, .value {
        width: 100%;
        height: fit-content;
    }

</style>