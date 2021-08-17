<script>
 // import Component
 import Katex from "./Katex.svelte";
 import ShowFirstItem from "./ShowFirstItem.svelte";
 import { onMount } from "svelte";
 
 let hash = {}

  let targetClasses = ['ex', 'ey', 'gxy']

 onMount(() => {
   targetClasses.forEach(className => {
   hash[className] = document.querySelectorAll(`.` + className)

     Object.values(hash).forEach(nodes => {
       nodes.forEach(node => {
         node.addEventListener('mouseover', () => nodes.forEach(n => n.classList.add('hovered')))
         node.addEventListener('mouseout', () => nodes.forEach(n => n.classList.remove('hovered')))
       })
     })
   })
 })

 // Math Equations
 let partial_strain = `
\\begin{align}
\\htmlClass{ex}{\\epsilon_{x}} = \\frac{\\partial u_x}{\\partial x} \\qquad
\\htmlClass{ey}{\\epsilon_{y}} = \\frac{\\partial u_y}{\\partial y} \\qquad
\\htmlClass{gxy}{\\gamma_{xy}} = \\frac{\\partial u_y}{\\partial x} + \\frac{\\partial u_x}{\\partial y}
\\end{align}
 `;

 let stress_strain = `
\\begin{align}
\\htmlClass{ex}{\\epsilon_x} = \\frac{1}{E}(\\sigma_x - \\nu \\sigma_y) \\qquad
\\htmlClass{ey}{\\epsilon_y} = \\frac{1}{E}(\\sigma_y - \\nu \\sigma_x) \\qquad
\\htmlClass{gxy}{\\gamma_{xy}} = \\frac{2(1 + \\nu)}{E}\\tau_{xy}
\\end{align}
`;

 let epsilon_x_diff = [
   `\\htmlClass{ex}{\\epsilon_{x}} = \\frac{\\partial u_x}{\\partial x}`,
   `\\frac{\\partial \\epsilon_x}{\\partial y} = \\frac{\\partial^2 u_x}{\\partial x \\partial y}`,
   `\\frac{\\partial^2 \\epsilon_x}{\\partial y^2} = \\frac{\\partial^3 u_x}{\\partial x \\partial y^2}`
 ]

 let epsilon_y_diff = [
   `\\htmlClass{ey}{\\epsilon_{y}} = \\frac{\\partial u_y}{\\partial y}`,
   `\\frac{\\partial \\epsilon_y}{\\partial x} = \\frac{\\partial^2 u_y}{\\partial y \\partial x}`,
   `\\frac{\\partial^2 \\epsilon_y}{\\partial x^2} = \\frac{\\partial^3 u_y}{\\partial y \\partial x^2}`
 ]

 let gamma_xy_diff = [
   `\\htmlClass{gxy name}{\\gamma_{xy}} = \\frac{\\partial u_y}{\\partial x} + \\frac{\\partial u_x}{\\partial y}`,
   `\\frac{\\partial \\gamma_{xy}}{\\partial x} = \\frac{\\partial^2 u_y}{\\partial x^2} + \\frac{\\partial^2 u_x}{\\partial x \\partial y}`,
   `\\frac{\\partial^2 \\gamma_{xy}}{\\partial x \\partial y} = \\frac{\\partial^3 u_y}{\\partial x^2 \\partial y} + \\frac{\\partial^3 u_x}{\\partial x \\partial y^2}`
 ]

 let axial_shear_sub = `
\\begin{aligned}
\\frac{\\partial^2 \\gamma_{xy}}{\\partial x \\partial y} &= \\frac{\\partial^3 u_y}{\\partial x^2 \\partial y} + \\frac{\\partial^3 u_x}{\\partial x \\partial y^2} \\\\
\\frac{\\partial^2 \\gamma_{xy}}{\\partial x \\partial y} &= \\frac{\\partial^2 \\epsilon_y}{\\partial x^2} + \\frac{\\partial^2 \\epsilon_x}{\\partial y^2} 
\\end{aligned}
 `

 let airys_func = `
\\begin{aligned}
\\sigma_x = \\frac{\\partial^2 \\phi}{\\partial y^2} \\qquad 
\\sigma_y = \\frac{\\partial^2 \\phi}{\\partial x^2} \\qquad
\\tau_{xy} = -\\frac{\\partial^2 \\phi}{\\partial x \\partial y}
\\end{aligned}
`

let epsilon_x_sub = [
  `\\htmlClass{ex}{\\epsilon_x} = \\frac{1}{E}(\\sigma_x - \\nu \\sigma_y)`,
  `\\htmlClass{ex}{\\epsilon_x} = \\frac{1}{E}\\left(\\frac{\\partial^2 \\phi}{\\partial y^2} - \\nu\\frac{\\partial^2 \\phi}{\\partial x^2}\\right)`,
  `\\frac{\\partial \\epsilon_x}{\\partial y} = \\frac{1}{E} \\left(\\frac{\\partial^3 \\phi}{\\partial y^3} - \\nu \\frac{\\partial^3\\phi}{\\partial x^2 \\partial y}\\right)`,
  `\\frac{\\partial^2 \\epsilon_x}{\\partial y^2} = \\frac{1}{E} \\left(\\frac{\\partial^4 \\phi}{\\partial y^4} - \\nu \\frac{\\partial ^4 \\phi}{\\partial x^2 \\partial y^2}\\right)`
]

let epsilon_y_sub = [
  `\\htmlClass{ey}{\\epsilon_y} = \\frac{1}{E}(\\sigma_y - \\nu \\sigma_x)`,
  `\\htmlClass{ey}{\\epsilon_y} = \\frac{1}{E}\\left(\\frac{\\partial^2 \\phi}{\\partial x^2} - \\nu\\frac{\\partial^2 \\phi}{\\partial y^2}\\right)`,
  `\\frac{\\partial \\epsilon_y}{\\partial x} = \\frac{1}{E} \\left(\\frac{\\partial^3 \\phi}{\\partial x^3} - \\nu \\frac{\\partial^3\\phi}{\\partial y^2 \\partial x}\\right)`,
 `\\frac{\\partial^2 \\epsilon_y}{\\partial x^2} = \\frac{1}{E} \\left(\\frac{\\partial^4 \\phi}{\\partial x^4} - \\nu \\frac{\\partial ^4 \\phi}{\\partial y^2 \\partial x^2}\\right)`
]

let gamma_xy_sub = [
  `\\htmlClass{gxy}{\\gamma_{xy}} = \\frac{2(1 + \\nu)}{E}\\tau_{xy}`,
  `\\htmlClass{gxy}{\\gamma_{xy}} = \\frac{2(1 + \\nu)}{E}\\left(-\\frac{\\partial^2 \\phi}{\\partial x \\partial y}\\right)`,
  `\\frac{\\partial \\gamma_{xy}}{\\partial x} =  \\frac{2(1 + \\nu)}{E}\\left(-\\frac{\\partial^3 \\phi}{\\partial x^2 \\partial y}\\right)`,
  `\\frac{\\partial^2 \\gamma_{xy}}{\\partial x \\partial y} = \\frac{2(1 + \\nu)}{E}\\left(-\\frac{\\partial^4 \\phi}{\\partial x^2 \\partial y^2}\\right)`
]

let biharmonic_eqn =`
\\nabla^4\\phi = \\frac{\\partial^4 \\phi}{\\partial x^4} + 2 \\frac{\\partial^4 \\phi}{\\partial x^2 \\partial y^2} + \\frac{\\partial^4 \\phi}{\\partial y^4} = 0
`
</script>

<main>
  <h1>Derivation of Airy's Stress Relationship with Biharmonic Equation</h1>
	<h2>Strain Partial Derivative Relationship (From 2D Strain Block) </h2>
  <Katex math={partial_strain} displayMode/>
  <h2>Stress/Strain Relationships in 2D</h2>
  <Katex math={stress_strain} displayMode/>
  <h2>Differentiation of <Katex math={"\\htmlClass{ex}{\\epsilon_x}"} /></h2>
  <ShowFirstItem entry={epsilon_x_diff} />
  <h2>Differentiation of <Katex math={"\\htmlClass{ey}{\\epsilon_y}"} /></h2>
  <ShowFirstItem entry={epsilon_y_diff} />
  <h2>Differentiation of <Katex math={"\\htmlClass{gxy}{\\gamma_{xy}}"} /></h2>
  <ShowFirstItem entry={gamma_xy_diff} />
  <h2>Substitution of Axial Strain into Shear Strain Equation</h2>
  <Katex math={axial_shear_sub} displayMode/>
  <h2>Airy's Stress Function Definitions</h2>
  <Katex math={airys_func} displayMode />
  <h2>Substitution of Airy's Stress Function into Stress/Strain Relationships</h2>
  <ShowFirstItem entry={epsilon_x_sub} />
  <ShowFirstItem entry={epsilon_y_sub} />
  <ShowFirstItem entry={gamma_xy_sub} />
  <h2>Biharmonic Equation</h2>
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
 :global(.hovered) {
   color: red
 }
</style>
