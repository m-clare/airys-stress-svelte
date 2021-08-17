<script>
  import Katex from "./Katex.svelte";
  export let entry
</script>

<style>
</style>

<ul style="list-style:none">
	{#each entry as item, i}
	    <li><Katex math={item} displayMode /></li>
	{/each}
</ul>


