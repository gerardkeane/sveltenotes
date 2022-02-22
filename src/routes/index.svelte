<script context="module">
    export async function load({params}, limit=150) {
        const url = `https://pokeapi.co/api/v2/pokemon?limit=${limit}`;
        const res = await fetch(url);
        const data = await res.json();
        const loadedPokemon = data.results.map((data, index) => {
            return {
                name: data.name,
                id: index + 1,
                image: `http://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${
                    index + 1
                }.png`
            };
        });
        return {props: {pokemon: loadedPokemon}}
    }
</script>

<script>
    // import {pokemon} from "../stores/pokestore"
    export let pokemon;
    import PokemanCard from "../components/pokemanCard.svelte";

    let searchTerm = ""
    let filteredPokemon = []

    $: {
        if(searchTerm) {
            filteredPokemon = pokemon.filter(pokeman => pokeman.name.toLowerCase().includes(searchTerm.toLowerCase()))
        }else {
            filteredPokemon = [...pokemon]
        }
    }
</script>

<svelte:head>
    <title>Pokedex</title>
</svelte:head>

<h1 class="text-4xl text-center my-8 uppercase font-bold">Pokedex</h1>

<input class="w-full rounded-md text-lg p-4 mb-4 border-2 border-gray-200" bind:value={searchTerm} type="text" placeholder="Search Pokemon">

<div class="grid gap-4 md:grid-cols-2 grid-cols-1">
    {#each filteredPokemon as pokeman}
    <PokemanCard pokeman={pokeman} />
    {/each}
</div>