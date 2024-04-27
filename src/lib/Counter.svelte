<script context="module">
  let totalCount = 0
  export function getTotalCount () {
    return totalCount
  }
</script>

<script>
  let count = 0
  function increment () {
    count += 1
    totalCount += 1
  }
</script>

<button on:click={increment}>
  count is {count}
</button>
