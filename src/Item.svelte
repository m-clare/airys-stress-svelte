<script>
  import { slide } from "svelte/transition";
  import Katex from "./Katex.svelte";
  export let entry
  let isOpen = false
  const toggle = () => isOpen = !isOpen
</script>

<style>
	button {border: none;
          background: none;
          display: block;
          color: inherit;
          font-size: 1em;
          cursor: pointer;
          margin: 0;
          padding: 0px;
         }

	svg { transition: transform 0.2s ease-in;
	}

	[aria-expanded=true] svg { transform: rotate(0.25turn); }
</style>

<ul style="list-style:none">
	{#each entry as item, i}
    {#if i === 0}
      <li><button on:click={toggle}
                  style="display: block;
                         width: 100%">
          <Katex math={entry[0]} displayMode/></button></li>
    {/if}
    {#if isOpen & i !==0}
	    <li transition:slide={{duration: 300}}><Katex math={item} displayMode /></li>
    {/if}
	{/each}
</ul>


