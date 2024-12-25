<script>
// Constants
const curve = {
	WN : "a 20 20 0 0 1 -20 -20",
	SW : "a 20 20 0 0 1 -20  20",
	NE : "a 20 20 0 0 1  20 -20",
	ES : "a 20 20 0 0 1  20  20",
	NW : "a 20 20 0 0 0 -20 -20",
	WS : "a 20 20 0 0 0 -20  20",
	EN : "a 20 20 0 0 0  20 -20",
	SE : "a 20 20 0 0 0  20  20",
	NWN: "a 25 25 0 0 1 -10 -20",
	WNW: "a 25 25 0 0 1 -20 -10",
	SSW: "a 25 25 0 0 1 -10  20",
	SWW: "a 25 25 0 0 1 -20  10",
	NNE: "a 25 25 0 0 1  10 -20",
	NEE: "a 25 25 0 0 1  20 -10",
	SES: "a 25 25 0 0 1  10  20",
	ESE: "a 25 25 0 0 1  20  10",
	NNW: "a 25 25 0 0 0 -10 -20",
	NWW: "a 25 25 0 0 0 -20 -10",
	SWS: "a 25 25 0 0 0 -10  20",
	WSW: "a 25 25 0 0 0 -20  10",
	NEN: "a 25 25 0 0 0  10 -20",
	ENE: "a 25 25 0 0 0  20 -10",
	SSE: "a 25 25 0 0 0  10  20",
	SEE: "a 25 25 0 0 0  20  10"
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
