<script lang="ts">
	function shakeBox(e: Event) {
		e.preventDefault;
		const box = e.currentTarget as HTMLElement;
		// -> and re-adding the class
		box.classList.add('shake');

		box.addEventListener('animationend', () => {
			box.classList.remove('shake');
			reset_animation(box);
		});
		shakes++;
	}

	function openBox(e: Event) {
		e.preventDefault;
		const box = e.currentTarget as HTMLElement;
		const lid = box.querySelector('.lid');
		const contents = box.querySelector('.contents');
		// -> and re-adding the class
		lid?.classList.add('open');
		contents?.classList.add('open');
	}

	function reset_animation(el: HTMLElement) {
		el.style.animation = 'none';
		el.offsetHeight; /* trigger reflow */
		el.style.animation = '';
	}

	let shakes = $state(0);
	const shakesToOpen = 3;
</script>

<button
	aria-label="container"
	class="box"
	onclick={shakes === shakesToOpen ? openBox : shakeBox}
	style="--shakes: {shakes}">
	<div class="lid"></div>
	<div class="contents"></div>
</button>

<style>
	.box {
		place-self: center;
		width: 20vh;
		aspect-ratio: 1 /1;
		position: relative;
		background-color: lightblue;
		cursor: pointer;
		animation: shake 0.4s;
		animation-play-state: paused;

		&:global(.shake) {
			animation-play-state: running;
		}

		.lid {
			position: absolute;
			top: -5%;
			height: 15%;
			width: 106%;
			left: -3%;
			background-color: blue;
			transition: all 1s;
			transform-origin: bottom right;

			&:global(.open) {
				rotate: 90deg;
				opacity: 0;
			}
		}
		.contents {
			display: none;
			opacity: 0;
			background-image: url(/containers/eevee.png);
			background-size: contain;
			background-repeat: no-repeat;
			background-position: center;
			cursor: default;

			&:global(.open) {
				display: block;
				animation: appear 1s ease-in-out both;
				width: 100%;
				height: 100%;
			}
		}
	}

	@keyframes shake {
		33% {
			rotate: calc(var(--shakes) * 5deg);
		}
		66% {
			rotate: calc(var(--shakes) * -5deg);
		}
		100% {
			rotate: 0deg;
		}
	}

	@keyframes appear {
		0% {
			z-index: 0;
			opacity: 0;
			scale: 0.5;
		}
		50% {
			opacity: 100%;
			z-index: 2;
			translate: 0 -200%;
		}
		100% {
			translate: 0 0;
			opacity: 100%;
			scale: 1.5;
		}
	}
</style>
