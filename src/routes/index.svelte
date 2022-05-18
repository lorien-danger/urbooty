<script lang="ts">
    import type { Person } from "../types/Person.type";
    import { faker } from "@faker-js/faker";
    import NamesList from "../components/NamesList.svelte";
    import ActionBar from "../components/ActionBar.svelte";

    const people: Person[] = createRandomPeople(100);
    let showAll = false;
    let loggedIn = false;
    let searchString: string = "";

    $: filteredPeople = returnFilteredPeople(searchString);

    function createRandomPeople(count: number) {
        const people: Person[] = [];

        for (let i = 0; i < count; i++) {
            people.push({
                firstName: faker.name.firstName(),
                lastName: faker.name.lastName(),
                ownership: faker.datatype.number({min: 1, max: 1000})
            });
        }

        return people;
    }

    function returnFilteredPeople(search: string): Person[] {
        console.log(people.filter(person => {
            return person.firstName.toLowerCase().includes(search.toLowerCase()) || person.lastName.toLowerCase().includes(search.toLowerCase());
        }))
    }
</script>

<div class={`${!showAll ? "h-screen pb-20" : ""} container mx-auto flex flex-col justify-center items-center font-sans text-zinc-900`}>
    <NamesList {people} {showAll} on:click={() => showAll = true} />
    <ActionBar {showAll} {loggedIn} on:input={(e) => searchString = e.target.value || ""} />
</div>