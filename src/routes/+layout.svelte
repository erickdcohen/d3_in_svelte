<script lang="ts">
	import '../app.css';
	let { children } = $props();
</script>

<h1 class="mt-4 ml-4 text-center text-3xl text-lime-300">
	Landing Practicing <a
		href="https://datavisualizationwithsvelte.com/"
		class="underline hover:text-lime-500"
		rel="no referer noopener"
		target="_blank">D3 in Svelte</a
	>
</h1>

<nav class="m-4">
	<ul class="flex flex-col">
		<a href="/" class="my-2 text-xl text-lime-300 underline hover:text-lime-500">Home</a>
		<a href="/basic-shapes" class="my-2 text-xl text-lime-300 underline hover:text-lime-500"
			>1. Basic Shapes</a
		>
	</ul>
</nav>

{@render children()}
