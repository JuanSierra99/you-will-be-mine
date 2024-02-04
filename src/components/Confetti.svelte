<script lang="ts">
	import Confetti from './Confetti.svelte';
	export let xOrigin: number;
	export let yOrigin: number;
	let popped = false;
	let poppedX: number;
	let poppedY: number;

	const randomizeAnimation = () => {
		const duration = Math.random() * 10 + 2;
		const delay = Math.random() * 3;
		return 'explosion 1s';
	};

	const halfScreen = screen.availHeight / 2;
	const halfWidth = screen.availWidth / 2;

	const randomSize = () => {
		return `${Math.random() * 8 + 2}px`;
	};

	const randomColor = () => {
		const colors = ['black', 'white', 'white'];
		const random = colors[Math.floor(randomBetween(0, 2))];
		return random;
	};

	const randomBetween = (minimum: number, maximum: number) => {
		return Math.random() * (maximum - minimum) + minimum;
	};

	let confettis: any;
	confettis = Array(200)
		.fill(null)
		.map((_, i) => {
			return {
				id: i,
				style: `
		--x-origin: ${xOrigin}px;
		--y-origin: ${yOrigin}px;
		--x-translate: ${randomBetween(-halfWidth, halfWidth)}px;
		--y-translate: ${randomBetween(-halfScreen, halfScreen - 200)}px;
		--animation-delay: ${randomBetween(0, 0.2)}s;
		--animation-duration: ${randomBetween(1, 2)}s;
		--rotation: ${randomBetween(-360, 360)}deg;
    `
			};
		});

	const clusterBombs = (id: number, event: MouseEvent) => {
		poppedX = event.clientX;
		poppedY = event.clientY;

		popped = true;
		confettis = confettis.filter((c) => c.id !== id);
	};
</script>

{#each confettis as c}
	<button style={c.style} class="confetti" on:click={(event) => clusterBombs(c.id, event)}>
		<img src="./heart-solid.svg" class="heart" alt="..." />
	</button>
{/each}

{#if popped}
	<Confetti xOrigin={poppedX} yOrigin={poppedY} />
{/if}

<style>
	.heart {
		width: 10px;
		height: auto;
	}

	.confetti {
		top: var(--y-origin);
		left: var(--x-origin);
		position: absolute;
		width: fit-content;
		height: auto;
		border: none;
		background-color: transparent;
		animation: explosion var(--animation-duration);
		animation-delay: var(--animation-delay);
		animation-fill-mode: forwards;
	}

	@keyframes explosion {
		0%,
		25%,
		50% {
			/* background-color: var(--confetti-color); */
		}
		75%,
		100% {
			transform: translate(var(--x-translate), var(--y-translate)) rotate(var(--rotation));
			/* background-color: transparent; */
		}
	}
</style>
