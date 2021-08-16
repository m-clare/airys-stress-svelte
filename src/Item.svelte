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
          padding-bottom: 0.5em;
          padding-top: 0.5em}

	svg { transition: transform 0.2s ease-in;
	}

	[aria-expanded=true] svg { transform: rotate(0.25turn); }
</style>

<button on:click={toggle}
        aria-expanded={isOpen}>
  <svg style="tran"
       width="15"
       height="15"
       fill="none"
       stroke-linecap="round"
       stroke-linejoin="round"
       stroke-width="1"
       viewBox="0 0 24 24"
       stroke="currentColor">
    <path d="M9 5l7 7-7 7"></path>
  </svg> <Katex math={entry[0]} displayMode />
</button>
{#if isOpen}
<ul style="list-style:none" transition:slide={{ duration: 300 }}>
	{#each entry[1] as item}
	<li><Katex math={item} displayMode /></li>
	{/each}
</ul>
{/if}

