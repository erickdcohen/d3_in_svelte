<script lang="ts">
	import { Tween } from 'svelte/motion';
	import { cubicOut } from 'svelte/easing';

	type Circle = {
		x: number;
		y: number;
		r: number;
		fill: string;
	};

	type Rectangle = {
		x: number;
		y: number;
		width: number;
		height: number;
	};

	let circles: Circle[] = $state([
		{ x: 180, y: 30, r: 5, fill: 'orange' },
		{ x: 100, y: 40, r: 25, fill: 'red' },
		{ x: 170, y: 160, r: 50, fill: 'cyan' },
		{ x: 120, y: 220, r: 2, fill: 'yellow' },
		{ x: 30, y: 100, r: 10, fill: 'purple' }
	]);

	let rectangles: Rectangle[] = $state([
		{ x: 10, y: 10, width: 5, height: 40 },
		{ x: 10, y: 60, width: 5, height: 40 },
		{ x: 10, y: 110, width: 5, height: 40 },
		{ x: 10, y: 160, width: 5, height: 40 },
		{ x: 10, y: 210, width: 5, height: 40 }
	]);

	let rectanglesText: Rectangle[] = $state([
		{ x: 10, y: 10, width: 5, height: 40 },
		{ x: 10, y: 60, width: 5, height: 40 },
		{ x: 10, y: 110, width: 5, height: 40 },
		{ x: 10, y: 160, width: 5, height: 40 },
		{ x: 10, y: 210, width: 5, height: 40 }
	]);

	const widths = Tween.of(() => rectanglesText.map((rec) => rec.width), {
		duration: 1000,
		easing: cubicOut
	});

	const handleClick = () => {
		rectanglesText = [
			{ x: 10, y: 10, width: 450 * Math.random(), height: 40 },
			{ x: 10, y: 60, width: 320 * Math.random(), height: 40 },
			{ x: 10, y: 110, width: 160 * Math.random(), height: 40 },
			{ x: 10, y: 160, width: 80 * Math.random(), height: 40 },
			{ x: 10, y: 210, width: 10 * Math.random(), height: 40 }
		];
	};

	// Circles transitions
	setTimeout(() => {
		circles = [
			{ x: 40, y: 70, r: 5, fill: 'red' },
			{ x: 100, y: 210, r: 25, fill: 'orange' },
			{ x: 200, y: 100, r: 50, fill: 'blue' },
			{ x: 350, y: 220, r: 2, fill: 'red' },
			{ x: 30, y: 190, r: 10, fill: 'white' }
		];
	}, 2000);

	// Rectangles transitions
	setTimeout(() => {
		rectangles = [
			{ x: 10, y: 10, width: 450, height: 40 },
			{ x: 10, y: 60, width: 320, height: 40 },
			{ x: 10, y: 110, width: 160, height: 40 },
			{ x: 10, y: 160, width: 80, height: 40 },
			{ x: 10, y: 210, width: 10, height: 40 }
		];
	}, 4000);
</script>

<h1 class="mb-4 text-center text-2xl text-lime-300">01 -- Basic Shapes</h1>

<!-- Circles -->
<div id="circles" class="text-center text-xl text-slate-100">
	<h2 class="text-2xl">Circles</h2>
	<div>
		<svg viewBox="0 0 600 300">
			{#each circles as c}
				<circle cx={c.x} cy={c.y} r={c.r} fill={c.fill} />
			{/each}
		</svg>
	</div>
</div>

<!-- Rectangles -->
<div id="rectangles" class="text-center text-xl text-slate-100">
	<h2 class="text-2xl">Rectangles</h2>
	<div>
		<svg viewBox="0 0 600 300">
			{#each rectangles as rec}
				<rect
					id="reg-rect"
					x={rec.x}
					y={rec.y}
					width={rec.width}
					height={rec.height}
					fill="white"
				/>
			{/each}
		</svg>
	</div>
</div>

<!-- Rectangles with Text -->
<div id="rectanglesText" class="text-center text-xl text-slate-100">
	<h2 class="text-2xl">Rectangles with Text</h2>
	<div>
		<svg viewBox="0 0 600 300">
			{#each rectangles as rec, i}
				<rect x={rec.x} y={rec.y} width={widths.current[i]} height={rec.height} fill="white" />
				<text
					fill="white"
					x={rec.x + widths.current[i] + 10}
					y={rec.y + rec.height / 2 + 5}
					text-anchor="start"
				>
					{widths.current[i].toFixed(0)}</text
				>
			{/each}
		</svg>
		<button
			onclick={handleClick}
			class="m-2 mb-10 rounded-lg bg-yellow-400 px-2 py-2 text-lg font-semibold text-gray-900 hover:bg-yellow-500"
			>Animate</button
		>
	</div>
</div>

<style>
	circle {
		transition: all 1s ease;
	}

	#reg-rect {
		transition: all 1s ease;
	}
</style>
