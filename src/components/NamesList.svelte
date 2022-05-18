<script lang="ts">
    import type { Person } from "../types/Person.type";
    import NameItem from "./NameItem.svelte";

    export let people: Person[] = [];
    export let showAll = false;
    export let cutOffAmount = 8;
</script>

<div class="pt-20 pb-14 flex flex-col text-center">
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
    <p class="mt-8 text-2xl font-semibold">own urbooty.</p>
</div>