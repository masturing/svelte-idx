<script>
    import { createEventDispatcher } from "svelte";

    const dispatch = createEventDispatcher()
    function greet() {
        dispatch('greet', 'halo')
    }
</script>

<button on:click={greet}>Greet</button>