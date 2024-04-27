<script>
    import { count } from "../stores/stores";

function increaseCount() {
    count.update(value => {
        return value + 1
    })
}
</script>

<button on:click={increaseCount}>Increase</button>