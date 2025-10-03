<script lang="ts">
	const themes = [
		{ name: 'transparency', active: true },
		{ name: 'maps', active: false },
		{ name: 'scramble', active: false },
		{ name: 'filters', active: false },
		{ name: 'remix', active: false },
		{ name: 'solids', active: false },
		{ name: 'sub-optimal', active: false },
		{ name: 'containers', active: false },
		{ name: 'blink', active: false },
		{ name: 'warning', active: false },
		{ name: 'camera', active: false },
		{ name: 'battle', active: false },
		{ name: 'upside-down', active: false },
		{ name: 'doubles', active: false },
		{ name: 'unicode', active: false },
		{ name: 'transition', active: false },
		{ name: 'illumination', active: false },
		{ name: 'trading', active: false },
		{ name: 'bounce', active: false },
		{ name: 'hidden', active: false },
		{ name: 'language', active: false },
		{ name: 'memory', active: false },
		{ name: 'style', active: false },
		{ name: 'counter', active: false },
		{ name: 'empty', active: false },
		{ name: 'texture', active: false },
		{ name: 'spell', active: false },
		{ name: 'tables', active: false },
		{ name: 'surprise', active: false },
		{ name: 'deprecated', active: false },
		{ name: 'spooky', active: false }
	];

	export const capitalize = (s: string) =>
		(s && String(s[0]).toUpperCase() + String(s).slice(1)) || '';
</script>

<svelte:head><title>Weird Web October 2025</title></svelte:head>
<hgroup>
	<h2>I'm participating in</h2>
	<a href="https://weirdweboctober.website/">
		<h1>Weird Web October 2025</h1>
	</a>
</hgroup>

<h3>Themes</h3>
<ol>
	{#each themes as theme}
		<li id={theme.name}>
			{#if theme.active}
				<a href={theme.name}>{capitalize(theme.name)}</a>
			{:else}
				<p>{capitalize(theme.name)}</p>
			{/if}
		</li>
	{/each}
</ol>

<style>
	ol {
		display: flex;
		flex-direction: column;
		flex-wrap: wrap;
		max-height: 80vh;
	}
</style>
