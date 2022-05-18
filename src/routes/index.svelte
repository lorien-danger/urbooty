<script lang="ts">
    import type { Person } from "../types/Person.type";
    import { faker } from "@faker-js/faker";
    import NamesList from "../components/NamesList.svelte";
    import ActionBar from "../components/ActionBar.svelte";

    const people: Person[] = createRandomPeople(400);
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
        return people.filter(person => {
            const fullName = `${person.firstName} ${person.lastName}`;
            return fullName.toLowerCase().includes(search.toLowerCase())
        });
    }
</script>

<div class="h-screen flex">
    <div class="container mx-auto grow flex flex-col justify-between items-center font-sans text-zinc-900">
        <NamesList people={filteredPeople} {showAll} {searchString} on:click={() => showAll = true} />
        <ActionBar {loggedIn} on:input={(e) => searchString = e.target.value || ""} />
    </div>
</div>