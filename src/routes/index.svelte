<script context="module">
    async function getData (limit = 150) {
        const promises = [];
        for (let i = 1; i <= limit; i++) {
            const url = `https://pokeapi.co/api/v2/pokemon/${i}`;
            promises.push(fetch(url).then(res => res.json()))
        }
        // console.log(promises)

        // console.log(Promise.all(promises).then(results => {
        //     console.log(results.map(data => ({
        //         name: data.name,
        //         id: data.id,
        //         image: data.sprites["front_default"],
        //         type: data.types.map(type => type.type.name).join(", "),
        //         ability: data.abilities.map(ability => ability.ability.name).join(','),
        //         moves: data.moves.map(move => move.move.name).slice(0, 10).join(', ')
        //     })))
        // })
        // )

        return Promise.all(promises).then(results => {
            return results.map(data => ({
                name: data.name,
                id: data.id,
                image: data.sprites["front_default"],
                type: data.types.map(type => type.type.name).join(", "),
                ability: data.abilities.map(ability => ability.ability.name).join(','),
                moves: data.moves.map(move => move.move.name).slice(0, 10).join(', ')
            }))
        })
        // const pokemon = Promise.all(promises).then(results => {
        //     return results.map(data => ({
        //         name: data.name,
        //         id: data.id,
        //         image: data.sprites["front_default"],
        //         type: data.types.map(type => type.type.name).join(", "),
        //         ability: data.abilities.map(ability => ability.ability.name).join(','),
        //         moves: data.moves.map(move => move.move.name).slice(0, 10).join(', ')
        //     }))
        // })
        // console.log(pokemon)
        // return pokemon
    }

    export async function load(limit = 150) {
        const promises = [];
        for (let i = 1; i <= limit; i++) {
            const url = `https://pokeapi.co/api/v2/pokemon/${i}`;
            promises.push(fetch(url).then(res => res.json()))
        }
        const data = await Promise.all(promises).then(results => {
            return results.map(data => ({
                name: data.name,
                id: data.id,
                image: data.sprites["front_default"],
                type: data.types.map(type => type.type.name).join(", "),
                ability: data.abilities.map(ability => ability.ability.name).join(','),
                moves: data.moves.map(move => move.move.name).slice(0, 10).join(', ')
            }))
        }).catch(error => console.log(`Error in promises ${error}`))
        // const data = getData()
        console.log("data", data)
        // const loadedPokemon = pokemon.results.map((pokemon) => {
        //     return {
        //         name: pokemon.name,
        //         id: pokemon.id,
        //         image: pokemon.sprites["front_default"],
        //         type: pokemon.types.map(type => type.type.name).join(", "),
        //         ability: pokemon.abilities.map(ability => ability.ability.name).join(','),
        //         moves: pokemon.moves.map(move => move.move.name).slice(0, 10).join(', ')
        //     };
        // });
        return {props: {pokemon: data}}
    }

    // export async function load(limit=150) {
    //     let data = []
    //     for (let i = 1; i <= limit; i++) {
    //         const url = `https://pokeapi.co/api/v2/pokemon/${i}`;
    //         // promises.push(fetch(url).then(res => res.json()))
    //         const res = await fetch(url);
    //         data.push(res.json());
    //     }
    //     console.log(data)
    //     const loadedPokemon = data.results.map((data, index) => {
    //         return {
    //             name: data.name,
    //             id: index + 1,
    //             image: `http://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${
    //                 index + 1
    //             }.png`
    //         };
    //     });
    //     return {props: {pokemon: loadedPokemon}}
    // }

    // export async function load({params}, limit=150) {
        //     const promises = [];
        //     for (let i = 1; i <= limit; i++) {
        //         const url = `https://pokeapi.co/api/v2/pokemon/${i}`;
        //         promises.push(fetch(url).then(res => res.json()))
        //     }
        //     const loadedPokemon = []
        //     const addPokemonToArray = (pokemon) => {
        //         loadedPokemon.push(pokemon)
        //     }
        //     Promise.all(promises).then(results => {
        //         const pokemon = results.map(data => ({
        //             name: data.name,
        //             id: data.id,
        //             image: data.sprites["front_default"],
        //             type: data.types.map(type => type.type.name).join(", "),
        //             ability: data.abilities.map(ability => ability.ability.name).join(','),
        //             moves: data.moves.map(move => move.move.name).slice(0, 10).join(', ')
        //         }))
        //         return pokemon
        //     }).then(pokemon => {
        //         addPokemonToArray(pokemon)
        //         console.log(loadedPokemon)
        //     })
    //     return {props: {pokemon: loadedPokemon}}
    // }

</script>

<script>
    // import {pokemon} from "../stores/pokestore"
    export let pokemon;
    import PokemanCard from "../components/pokemanCard.svelte";

    // let searchTerm = ""
    // let filteredPokemon = []

    // $: {
    //     if(searchTerm) {
    //         filteredPokemon = pokemon.filter(pokeman => pokeman.name.toLowerCase().includes(searchTerm.toLowerCase()))
    //     }else {
    //         filteredPokemon = [...pokemon]
    //     }
    // }
</script>

<svelte:head>
    <title>Pokedex</title>
</svelte:head>

<h1 class="text-4xl text-center my-8 uppercase font-bold">Pokedex</h1>

<!-- <input class="w-full rounded-md text-lg p-4 mb-4 border-2 border-gray-200" bind:value={searchTerm} type="text" placeholder="Search Pokemon"> -->

<div class="grid gap-4 md:grid-cols-2 grid-cols-1">
    {#each pokemon as pokeman}
    <!-- {#each filteredPokemon as pokeman} -->
    <PokemanCard pokeman={pokeman} />
    {/each}
</div>