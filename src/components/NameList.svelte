<script>
    const names = [
        {
            firstName: "Bobby",
            lastName: "Indra"
        },
        {
            firstName: "John",
            lastName: "Doe"
        }
    ]
</script>

{#each names as {firstName, lastName}}
<slot name="hero" firstName={firstName} lastName={lastName} />
{/each}