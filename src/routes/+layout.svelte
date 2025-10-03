<script lang="ts">
	import favicon from '$lib/assets/favicon.svg';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<div class="page">
	<header><a href="/">Home</a></header>
	{@render children?.()}
</div>

<style>
	:global(body) {
		margin: 0;
	}

	.page {
		min-height: 100vh;
		display: grid;
		grid-template-rows: min-content;
		grid-auto-rows: auto;

		header {
			background-color: rgb(255, 220, 226);
			padding: 0.5rem 1rem;
		}
	}
</style>
