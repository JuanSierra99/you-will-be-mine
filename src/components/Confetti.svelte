<script lang="ts">
	const randomizeAnimation = () => {
		const duration = Math.random() * 10 + 2;
		const delay = Math.random() * 3;
		return 'explosion 1s';
	};

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
	confettis = Array(50)
		.fill(null)
		.map((_, i) => {
			return {
				id: i,
				style: `
		--x-translate: ${randomBetween(-400, 500)}px;
		--y-translate: ${randomBetween(-400, 500)}px;
		--animation-delay: ${randomBetween(0, 0.2)}s;
		--animation-duration: ${randomBetween(1, 2)}s;
		--rotation: ${randomBetween(-360, 360)}deg;
    `
			};
		});

	const explodeAgain = (id: number) => {
		confettis = confettis.filter((c) => c.id !== id);
	};
</script>

{#each confettis as c}
	<button style={c.style} class="confetti" on:click={() => explodeAgain(c.id)}>
		<img src="./heart-solid.svg" class="heart" alt="..." />
	</button>
{/each}

<style>
	.heart {
		width: 10px;
		height: auto;
	}

	.confetti {
		position: absolute;
		width: auto;
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
