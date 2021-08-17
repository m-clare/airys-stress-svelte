<script>
 // import Component
 import Katex from "./Katex.svelte";
 import Item from "./Item.svelte";
 import { onMount } from "svelte";
 let hash = {}

 onMount(() => {
   hash['test'] = document.querySelectorAll(`.test`)

   Object.values(hash).forEach(nodes => {
     nodes.forEach(node => {
       node.addEventListener('mouseover', () => nodes.forEach(n => n.classList.add('hovered')))
       node.addEventListener('mouseout', () => nodes.forEach(n => n.classList.remove('hovered')))
     })
   })
 })

 // Math Equations
 let partial_strain = `
\\begin{align}
\\epsilon_{x} = \\frac{\\partial u_x}{\\partial x} \\qquad
\\epsilon_{y} = \\frac{\\partial u_y}{\\partial y} \\qquad
\\gamma_{xy} = \\frac{\\partial u_y}{\\partial x} + \\frac{\\partial u_x}{\\partial y}
\\end{align}
 `;

 let stress_strain = `
\\begin{aligned}
\\epsilon_x = \\frac{1}{E}(\\sigma_x - \\nu \\sigma_y) \\qquad
\\epsilon_y = \\frac{1}{E}(\\sigma_y - \\nu \\sigma_x) \\qquad
\\gamma_{xy} = \\frac{2(1 + \\nu)}{E}\\tau_{xy}
\\end{aligned}
`;


 const e_x = {
   "test" : [
     `\\frac{\\partial \\epsilon_x}{\\partial y} = \\frac{\\partial^2 u_x}{\\partial x \\partial y}`,
     `\\frac{\\partial^2 \\epsilon_x}{\\partial y^2} = \\frac{\\partial^3 u_x}{\\partial x \\partial y^2}`
   ]
 }

 const y_x = {
   'test': [
     0, 1
   ]
 }


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
 let eqnArray = [
   `\\htmlClass{test}{\\epsilon_{x}} = \\frac{\\partial u_x}{\\partial x}`,
   `\\frac{\\partial \\epsilon_x}{\\partial y} = \\frac{\\partial^2 u_x}{\\partial x \\partial y}`,
   `\\frac{\\partial^2 \\epsilon_x}{\\partial y^2} = \\frac{\\partial^3 u_x}{\\partial x \\partial y^2}`
 ]

</script>

<main>
  <h1>Derivation of Airy's Stress Relationship with Biharmonic Equation</h1>
	<h2>Strain Partial Derivative Relationship (From 2D Strain Block) </h2>
  <Katex math={partial_strain} displayMode/>
  <h2>Stress/Strain Relationships in 2D</h2>
  <Katex math={stress_strain} displayMode/>
  <h2>Differentiation of <Katex math="\epsilon_x" /></h2>
  <Item entry={eqnArray} />
  <h2>Differentiation of <Katex math="\epsilon_y" /></h2>
  <h2>Differentiation of <Katex math={"\\gamma_{xy}"} /></h2>
  <h2>Substitution of Axial Strain into Shear Strain Equation</h2>
  <h2>Airy's Stress Function Definition</h2>
  <h2>Substitution of Airy's Stress Function into Stress/Strain Relationships</h2>
  <h3><Katex math="\epsilon_x" /></h3>
  <h3><Katex math="\epsilon_y" /></h3>
  <h3><Katex math={"\\gamma_{xy}"} /></h3>
  <h2>Biharmonic Equation</h2>


	<p><Katex math={eq1} displayMode /> </p>
	<h2>Differentiation of <Katex math={name} /></h2>
	<p><Katex math={eq2} displayMode /></p>
	<h2>Stress/Strain Relationships in 2D</h2>
  <ul style="list-style-type:none;">
    {#each eqnArray as eqn, i}
    <li><button><Katex math={eqn} displayMode/></button></li>
    {/each}
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
