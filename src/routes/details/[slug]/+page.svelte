<script lang="ts">
    
    /** @type {import('./$types').PageData} */
    /** @type {import('./$types').PageLoad} */
    import { page } from '$app/stores';
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

    {#if pokemonData !== null}
    <div class="pokemonDatasContainer">
        <div class="pokemonPictureContainer">
            <h1>{pokemonData.name}</h1>
            <img src={pokemonData.sprites.front_shiny} alt={pokemonData.name} class="pokemonPicture"/>
        </div>
        <div class="pokemonStatsContainer">
            <div class="stats">
                <span class="numberStats">Number : {pokemonData.order}</span>
                <div class="statsContainer">
                    <div class="label">Types : </div>
                    <div class="value">{pokemonData.types[0].type.name}</div>
                </div>
            </div>
        </div>
    </div>
    {:else}
        <p>Loading...</p>
    {/if}

<style>

    .pokemonPicture {
        width: 300px;
        border-radius: 16px;
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