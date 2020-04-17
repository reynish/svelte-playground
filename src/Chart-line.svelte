<script>

  export let name;

  import { scaleLinear } from 'd3-scale';
	
  import points from './data.js';

	const yTicks = [0, 2, 4, 6, 8];
	const xTicks = [1980, 1990, 2000, 2010];
  const pad = {x:5,y:0};

	let width = 500;
	let height = 200;

  let tooltip = {x:0,y:0, show: false};

  $: xScale = scaleLinear()
		.domain([minX, maxX])
		.range([pad.x, width - pad.x]);

	$: yScale = scaleLinear()
		.domain([Math.min.apply(null, yTicks), Math.max.apply(null, yTicks)])
		.range([height, 0]);
  
  $: minX = points[0].x;
	$: maxX = points[points.length - 1].x;
  
  $: path = `M${points.map(p => `${xScale(p.x)},${yScale(p.y)}`).join('L')}`;
</script>

<svg viewBox="0 0 {width} {height}">
  {#each points as p, i}
    <rect
      class="bar"
      x="{xScale(p.x) - 5}"
      y="{yScale(p.y) - 10}"
      width="{10}"
      height="{20}"
      on:click={e => tooltip = { x: xScale(p.x) - 5, y: yScale(p.y) - 5, year: p.x, value: p.y, show: true }}
    ></rect>
  {/each}
  <path class="path-line" d={path} pointer-events="none"></path>
  <text x={tooltip.x} y={tooltip.y} visibility="{tooltip.show ? 'visible' : 'hidden'}">{tooltip.year}</text>
</svg>


<style>
  div { 
    display: inline
  }
  
	.path-line {
		fill: none;
		stroke: rgb(86,95,246);
		stroke-linejoin: round;
		stroke-linecap: round;
		stroke-width: 2;
	}
  
  .bar {
    fill: rgb(179,184,252)
  }
</style>