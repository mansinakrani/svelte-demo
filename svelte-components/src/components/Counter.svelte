<script context="module">
  // variables defined in module scripts are not reactive so to over come this to update data when values are updates we need to use stores
  let totalCount = 0
  export function getTotalCount() {
    return totalCount
  }
</script>

<script>
  let count = 0
  function clickHandler() {
    count += 1
    totalCount += 1
  }
</script>

<h2>Count - {count}</h2>
<button on:click={clickHandler}>Increment</button>