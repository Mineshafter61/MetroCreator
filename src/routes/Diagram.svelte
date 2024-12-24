<script>
let color = "red";
let path = "M250,250 h250 q 20 0, 20 20 v250";
</script>

<h1>Canvas Test</h1>
<div class="diagram">
	<svg aria-hidden="true" viewBox="0 0 1000 1000">
		<path d={path} stroke={color} />
	</svg>
</div>

<style>
	.diagram {
		display:flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.9;
	}

	svg {
		width: 100%;
		height: 100%;
	}
	
	path {
		vector-effect: non-scaling-stroke;
		stroke-width: 4px;
		fill: transparent;
	}
</style>
