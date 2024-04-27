<!-- <script>
    export let isShow
</script> -->

<div class="card">
    <div class="card-header">
        <slot name="header"></slot>
    </div>
    <div class="card-body">
        <slot name="body"></slot>
    </div>
    {#if $$slots.footer}
    <hr>
    <div class="card-footer">
        <slot name="footer"></slot>
    </div>
    {/if}
</div>

<style>
    .card {
        width: 100px;
        height: 100px;
        background-color: white;
        border-radius: 10px;
        border: 1px solid black;
        color: black;
    }
</style>