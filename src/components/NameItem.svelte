<script lang="ts">
    import type { Person } from "../types/Person.type";

    export let person: Person;
</script>

<li>
    <p>{person.firstName} {person.lastName}</p>
</li>