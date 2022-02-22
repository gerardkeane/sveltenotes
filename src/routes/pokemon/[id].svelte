<script context="module">
    export async function load({params}) {
        const id = params.id;
        const url = `https://pokeapi.co/api/v2/pokemon/${id}`;
        const res = await fetch(url)
        const data = await res.json()
        return {props: {data}}
    }
</script>

<script>
    export let data;
    const type = data.types.map(type => type.type.name).join(", ")
    const abilities = data.abilities.map(ability => ability.ability.name).join(', ')
    const heldItems = data.held_items.map(item => item.item.name).join(", ")
</script>

<div class="flex flex-col items-center">
    <h1 class="text-4xl font-bold uppercase my-8 text-center">{data.name} </h1>
    <img class="card-image w-96 h-96" src={data.sprites['front_default']} alt={data.name} />
    <p>Type: <strong>{type}</strong> | Height: <strong>{data.height}</strong> | Weight: <strong>{data.weight}</strong></p>
    <p>Abilities: <strong>{abilities}</strong></p>
    <p>Held Items:
        {#if heldItems.length}
        <strong>{heldItems}</strong>
        {:else}
        <strong>None</strong>
        {/if}
    </p>
</div>