<script>
    import { getContext } from "svelte";

    export let name
    export let hoby = 'default'
</script>

<h2>Hello {name} and hoby {hoby}</h2>
<p>{getContext("token")}</p>