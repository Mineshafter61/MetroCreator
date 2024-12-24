<script>
// Constants
const curve = {
	SW: "q 0  20,-20  20",
	SE: "q 0  20, 20  20",
	NW: "q 0 -20,-20 -20",
	NE: "q 0 -20, 20 -20",
	WN: "q -20 0,-20 -20",
	WS: "q -20 0,-20  20",
	EN: "q  20 0, 20 -20",
	ES: "q  20 0, 20  20"
};

const dir = {
	N : 1,
	S : 2,
	E : 4,
	W : 8,
	NE: 1 | 4,
	SE: 2 | 4,
	NW: 1 | 8,
	SW: 2 | 8
};

// Line maker
const makeLine = (/** @type {number} */ length, /** @type {number} */ direction) => {
	switch (direction) {
		case dir.N:
			return `v -${length}`;
		case dir.S:
			return `v ${length}`;
		case dir.E:
			return `h ${length}`;
		case dir.W:
			return `h -${length}`;
		case dir.NE:
			return `l ${length} -${length}`;
		case dir.SE:
			return `l ${length} ${length}`;
		case dir.NW:
			return `l -${length} -${length}`;
		case dir.SW:
			return `l -${length} ${length}`;
		default:
			return ``;
	}
};

let color = "red";
let path = ["M500,500", makeLine(100, dir.E), curve.EN, curve.NE, curve.ES, makeLine(100, dir.S), curve.SW, curve.WN, curve.NE, makeLine(100, dir.E)].join(" ");

// Grid generator
let circleCoords = []
for (let i = 0; i <= 1000; i += 10) for (let j = 0; j <= 1000; j += 10) {
	circleCoords.push([i, j])
}
</script>

<h1>Canvas Test</h1>
<div class="diagram">
	<svg viewBox="0 0 1000 1000">
		<!-- Grid generator -->
		{#each circleCoords as ccoord}
			<circle cx={ccoord[0]} cy={ccoord[1]} r="1" fill="gray" />
		{/each}

		<!-- Path generator -->
		<path d={path} stroke={color} />
	</svg>
</div>

<style>
	.diagram {
		display:flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}

	svg {
		border: solid;
	}
	
	path {
		vector-effect: non-scaling-stroke;
		stroke-width: 4px;
		fill: transparent;
	}
</style>
