<script lang="ts">
    import type { Person } from "../types/Person.type";
    import NameItem from "./NameItem.svelte";

    export let people: Person[] = [];
    export let showAll = false;
    export let searchString = "";
    export let cutOffAmount = 8;
</script>

<div class="pt-20 pb-14 grow flex flex-col justify-center text-center">
    {#if people.length > 0}
        <ul class="text-3xl font-bold flex flex-col gap-3">
            {#each people as person, i}
                {#if i < cutOffAmount || showAll}
                    <NameItem {person} />
                {:else if i === cutOffAmount}
                    <li>
                        <button on:click class="transition-all font-bold border-b-0 border-zinc-300 hover:border-b-4">+ {people.length - cutOffAmount} others</button>
                    </li>
                {/if}
            {/each}
        </ul>
        <p class="mt-8 text-2xl font-semibold">{people.length === 1 ? "owns urbooty." : "own urbooty."}</p>
    {:else}
        <p class="text-3xl font-semibold">{searchString}</p>
        <p class="mt-8 text-2xl font-semibold">doesn't own urbooty.</p>
    {/if}
</div>