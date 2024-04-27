<script>
    import { onDestroy } from "svelte";
    import { count } from "../stores/stores";

    let counter 
    const counterRx = count.subscribe((value) => {
        counter = value
    })
    onDestroy(counterRx)
</script>

<div>
<h3>Current count: {counter}</h3>
</div>