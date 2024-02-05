<script lang="ts">
	import Confetti from './Confetti.svelte';
	export let xOrigin: number;
	export let yOrigin: number;
	export let confettiAmmount: number;
	export let displace: boolean;
	export let vanish: boolean;
	export let colors: Array<string> = [];
	let cluster = false;
	let clusterX: number;
	let clusterY: number;

	const halfScreen = screen.availHeight / 2;
	const halfWidth = screen.availWidth / 2;

	const randomSize = () => {
		return `${Math.random() * 8 + 2}px`;
	};

	const getColor = () => {
		if (colors.length > 0) {
			return colors[Math.floor(randomBetween(0, colors.length))];
		} else {
			return '#d62828';
		}
	};

	const randomBetween = (minimum: number, maximum: number) => {
		return Math.random() * (maximum - minimum) + minimum;
	};

	let confettis: any;
	confettis = Array(confettiAmmount)
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
		--animation-fill: ${displace ? 'none' : 'forwards'};
		--dissapear: ${vanish ? '0' : '1'};

    `
			};
		});

	const clusterBombs = (id: number, event: MouseEvent) => {
		clusterX = event.clientX;
		clusterY = event.clientY;
		cluster = true;
		setTimeout(() => {
			cluster = false;
		}, 1000);
		confettis = confettis.filter((c) => c.id !== id);
	};
</script>

{#each confettis as c}
	<button style={c.style} class="confetti" on:click={(event) => clusterBombs(c.id, event)}>
		<!-- <svg src="./heart-solid.svg" class="heart" alt="..." /> -->
		<svg class="heart" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512">
			<!--!Font Awesome Free 6.5.1 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.-->
			<path
				fill={getColor()}
				d="M47.6 300.4L228.3 469.1c7.5 7 17.4 10.9 27.7 10.9s20.2-3.9 27.7-10.9L464.4 300.4c30.4-28.3 47.6-68 47.6-109.5v-5.8c0-69.9-50.5-129.5-119.4-141C347 36.5 300.6 51.4 
				268 84L256 96 244 84c-32.6-32.6-79-47.5-124.6-39.9C50.5 55.6 0 115.2 0 185.1v5.8c0 41.5 17.2 81.2 47.6 109.5z"
			/>
		</svg>
	</button>
{/each}

{#if cluster}
	<Confetti
		xOrigin={clusterX}
		yOrigin={clusterY}
		confettiAmmount={10}
		vanish={true}
		colors={[
			'#c1121f',
			'#eb5e28',
			'#fcca46',
			'#a1c181',
			'#4361ee',
			'#7209b7',
			'#e4c1f9',
			'#43aa8b',
			'#2c6e49',
			'#ff7b00',
			'#bbd0ff'
		]}
	/>
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
		animation-fill-mode: var(--animation-fill);
	}

	@keyframes explosion {
		from {
		}
		to {
			transform: translate(var(--x-translate), var(--y-translate)) rotate(var(--rotation));
			opacity: var(--dissapear);
		}
	}
</style>
