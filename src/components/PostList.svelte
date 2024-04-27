<script>
    import { onMount } from "svelte";

    let posts = []
    onMount(() => {
        fetch("https://jsonplaceholder.typicode.com/posts")
            .then(res => res.json())
            .then(data => posts = data)
    })
</script>

{#each posts as post (post.id)}
<h3>{post.id} - {post.title}</h3>
<p>{post.body}</p>
{:else}
<p>Loading...</p>
{/each}