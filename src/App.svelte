<script>
 // import Component
 import Katex from "./Katex.svelte";
 import { onMount } from "svelte";
 let hash = {}

 onMount(() => {
   hash['test'] = document.querySelectorAll(`.test`)
   console.log(hash['test'].length)

   Object.values(hash).forEach(nodes => {
     nodes.forEach(node => {
       node.addEventListener('mouseover', () => nodes.forEach(n => n.classList.add('hovered')))
       node.addEventListener('mouseout', () => nodes.forEach(n => n.classList.remove('hovered')))
     })
   })
 })

  // Math equations
 let name = `\\epsilon_x`;
 let eq1 = `\\htmlClass{test}{\\epsilon_x} = \\frac{\\partial u_x}{\\partial u_y}`;
 let eq2 = `
    \\begin{align} 
    \\htmlClass{test}{\\epsilon_{x}} &= \\frac{\\partial u_x}{\\partial x} \\\\
	  \\frac{\\partial \\epsilon_x}{\\partial y} &= \\frac{\\partial^2 u_x}{\\partial x \\partial y} \\\\
	  \\frac{\\partial^2 \\epsilon_x}{\\partial y^2} &= \\frac{\\partial^3 u_x}{\\partial x \\partial y^2} \\\\
	  \\end{align}
 `;
 let eq3 = `
	  \\htmlClass{test}{\\epsilon_x} = \\frac{1}{E}(\\sigma_x - \\nu \\sigma_y)
 `;
 let eq4 = `
 \\htmlClass{test}{\\epsilon_{x}} = \\frac{\\partial u_x}{\\partial x} \\
`;
  let eq5 = `
\\frac{\\partial \\epsilon_x}{\\partial y} = \\frac{\\partial^2 u_x}{\\partial x \\partial y} \\
`;
  let eq6 = `
	  \\frac{\\partial^2 \\epsilon_x}{\\partial y^2} = \\frac{\\partial^3 u_x}{\\partial x \\partial y^2} \\
`;
</script>

<main>
	<h2>Strain Partial Relationship</h2>
	<p><Katex math={eq1} displayMode /> </p>
	<h2>Differentiation of <Katex math={name} /></h2>
	<p><Katex math={eq2} displayMode /></p>
	<h2>Stress/Strain Relationships in 2D</h2>
  <ul>
	<li><Katex math={eq3} displayMode /></li>
  <li style="display: none"><Katex math={eq4} displayMode /></li>
  <li style="display: none"><Katex math={eq5} displayMode /></li>
  <li><Katex math={eq6} displayMode /></li>
  </ul>
</main>

<style>
 main {
		 text-align: center;
		 padding: 1em;
		 max-width: 240px;
		 margin: 0 auto;
 }

 /* h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	  } */

 @media (min-width: 640px) {
		 main {
			   max-width: 500px;
		 }
 }
 :global(.test.hovered) {
   background-color: red
 }
</style>
