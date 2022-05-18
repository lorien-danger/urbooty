<script>
    import { Icon, Plus, Search, User } from "svelte-hero-icons";

    export let loggedIn = false;
</script>

<div class="sticky shrink-0 bottom-0 px-4 pb-6 pt-0 flex justify-center bg-white w-full h-24">
    <button class="h-full w-24 flex justify-center items-center bg-zinc-900 text-zinc-50 hover:bg-zinc-800">
        <Icon src={loggedIn ? User : Plus} solid class="h-6 w-auto" />
    </button>
    <span class="h-full border-4 border-zinc-900 text-xl flex justify-center items-center">
        <Icon src={Search} solid class="pl-4 h-6 w-auto" />
        <input on:input class="outline-none font-medium  px-4 placeholder:font-normal placeholder:text-zinc-500" type="text" placeholder="Search for someone" />
    </span>
</div>