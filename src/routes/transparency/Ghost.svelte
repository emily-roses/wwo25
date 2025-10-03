<script lang="ts">
	import { onMount } from 'svelte';
	import type { MouseEventHandler } from 'svelte/elements';

	const { index, onBust }: { index: number; onBust: () => void } = $props();

	let busted = $state(false);

	const handleKill: MouseEventHandler<HTMLDivElement> = (el) => {
		if (!busted) {
			busted = true;
			(el.target as Element).classList.add('dead');
			onBust();
		}
	};

	const yPos = Math.random() * 70 + 'vh';
	const delay = Math.random() * 15 - 10 + 's';

	const moveSpeed = Math.random() * 30 + 15 + 's';

	onMount(() => {
		const ghost = document.querySelector('#ghost_' + index) as HTMLElement;
		ghost.style.setProperty('top', yPos);

		ghost.style.setProperty('animation-delay', delay);
		ghost.style.setProperty('animation-duration', moveSpeed + ', 1.5s');
	});
</script>

<!-- svelte-ignore a11y_click_events_have_key_events, a11y_no_static_element_interactions (because of reasons) -->
<div id={'ghost_' + index} class="ghost" onclick={handleKill}></div>

<style>
	.ghost {
		position: absolute;
		width: 51px;
		height: 73px;
		right: -5vw;
		top: 0;
		background-repeat: no-repeat;
		background-image: url(/transparency/ghost_normal.png);
		animation:
			translate 30s infinite linear,
			upDown 1.5s alternate infinite ease-in-out;
		animation-composition: add, accumulate;
		opacity: 40%;
		scale: 1.5;

		&:hover {
			background-image: url(/transparency/ghost_spotted.png);
		}
	}
	:global(.ghost.dead) {
		background-image: url(/transparency/ghost_dead.png) !important;
		animation-play-state: paused, paused;
	}

	@keyframes upDown {
		to {
			transform: translatey(100px);
		}
	}
	@keyframes translate {
		to {
			transform: translatex(-110vw);
		}
	}
</style>
