<script>
    import { fade } from "svelte/transition"
    export let pokeman;
</script>

<a sveltekit:prefetch class="p-6 bg-gray-200 text-black text-center rounded-md shadow-sm hover:shadow-lg flex flex-col items-center"
    href={`/pokemon/${pokeman.id}`} transition:fade>
    <img class="w-44 h-44" src={pokeman.image} alt={pokeman.name}>
    <h2 class="uppercase text-xl font-bold">{pokeman.name}</h2>
</a>