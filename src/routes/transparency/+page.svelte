<script lang="ts">
	import { onMount } from 'svelte';
	import Ghost from './Ghost.svelte';

	onMount(() => {
		const root = document.documentElement;
		document.addEventListener('pointermove', (ev) => {
			const position: [number, number] = [ev.clientX, ev.clientY];
			root.style.setProperty('--mouse-x', position[0] + 'px');
			root.style.setProperty('--mouse-y', position[1] - 30 + 'px');
		});
	});

	let numBusted = $state(0);
	const total = 10;

	const handleBust = () => {
		numBusted++;
	};
</script>

<svelte:head>
	<title>Ghostbustin'</title>
</svelte:head>
<main>
	<link rel="prefetch" href="/transparency/ghost_spotted.png" />
	<link rel="prefetch" href="/transparency/ghost_dead.png" />
	<div class="score">
		<span class="busted">{numBusted}</span>/<span class="total">{total}</span>
	</div>
	{#each { length: total }, index}
		<Ghost {index} onBust={handleBust} />
	{/each}
	<div class={numBusted < total ? 'overlay' : 'busted'}></div>
</main>

<style>
	:root {
		--mouse-x: 0;
		--mouse-y: 0;
		overflow: hidden;
	}
	main {
		background-color: #37474f;
		background-image: url('https://unsplash.com/photos/d-8_X7Ffxj4/download?ixid=M3wxMjA3fDB8MXxzZWFyY2h8NHx8aGF1bnRlZCUyMGhvdXNlJTIwaW50ZXJpb3J8ZW58MHx8fHwxNzU5NTA5NTYxfDA&force=true&w=1920');
		position: relative;
		display: grid;

		&:has(.overlay) {
			cursor: crosshair;
		}
	}
	.overlay {
		height: 100%;
		width: 100%;
		mask: radial-gradient(
				circle at var(--mouse-x) var(--mouse-y),
				rgba(110, 11, 11, 0) 0%,
				rgba(0, 0, 0, 1) 10%
			)
			left top no-repeat;
		background: black;
		pointer-events: none;
	}
	.overlay,
	main,
	.busted {
		background-size: cover;
		background-position: center;
	}
	.busted {
		background-image: url(/transparency/ghosts_busted.png);
	}
	.score {
		position: absolute;
		font-size: 2rem;
		font-weight: 800;
		color: white;
		z-index: 2;
		text-align: center;
		justify-self: center;

		span {
			font-size: 3rem;
		}
	}
</style>
