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
        console.log(pokemonData.types[0].type.name)
    }
</script>
    <Layout>
        {#if pokemonData !== null}
        <section class="section">
        <div class="pokemonDatasContainer">
            <div class="pokemonPictureContainer">
                <h1>{pokemonData.name}</h1>
                <img class="pokemonPicture" src={"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/"+pokemonData.id+".png"} alt={pokemonData.name}/>
            </div>
            <div class="pokemonStatsContainer">
                <div class="stats">
                    <span class="numberStats">Number : {pokemonData.order}</span>
                    <div class="statsContainer">
                        <div class="label">Types : </div>
                        <div class="value">{pokemonData.types[0].type.name}</div>
                    </div>
                    <div class="statsContainer">
                        <div class="label">Attaques : </div>
                        <div class="value">
                            <ul>
                                <li>{pokemonData.moves[0]?.move.name}</li>
                                <li>{pokemonData.moves[1]?.move.name}</li>
                                <li>{pokemonData.moves[2]?.move.name}</li>
                                <li>{pokemonData.moves[3]?.move.name}</li>
                            </ul>
                        </div>
                        
                    </div>
                </div>
            </div>
        </div>
    </section>

        {:else}
            <p>Loading...</p>
        {/if}
    </Layout>


<style>

    .pokemonPictureContainer {
        background-color: #F2F2F2;
        border-radius: 16px;
        padding: 16px;
    }

    .pokemonPictureContainer > h1 {
        color: black;
        text-align: center;
        margin-bottom: 0;
        text-transform: capitalize;
    }

    .pokemonPicture {
        width: 100%;
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
    }

    .stats {
        margin: auto;
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