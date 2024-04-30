<script>
  import { onMount } from 'svelte'
  let inputRef
  onMount(() => {
    inputRef.focus()
  })
</script>

<!-- readonly this binding applies to every element and allows to update the ref to the rendered element-->
<input type="text" bind:this={inputRef} />