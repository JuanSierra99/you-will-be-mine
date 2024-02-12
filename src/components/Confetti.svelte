<script lang="ts">
	import Confetti from './Confetti.svelte';
	export let xOrigin: number; // Starting x poistion of confetti, retlative to container it is in.
	export let yOrigin: number; // starting y position of confetti, relative to container it is in.
	export let confettiAmmount: number; // The number of individual confetti pieces
	export let displace: boolean;
	export let vanish: boolean; // True means confetti will vanish away as part of the animation.
	export let colors: Array<string> = []; // An array of random colors for each confetti piece, which wll be applied randomly.
	export let xDomain: [number, number]; // Range it will travel in px in x-direction
	export let yDomain: [number, number]; // Range it will travel in px in y-direction
	export let animationDuaration: [number, number];
	export let showOverflow: boolean; // Determines if it shows outside of container it is in
	export let clusterBomb = false; // Determines if it will burst into clusters when clicked

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

	// Initialize an array of n confetti pieces. Each piece has an id so that they can be individually removed if clicked.
	let confettis: any;
	confettis = Array(confettiAmmount)
		.fill(null)
		.map((_, i) => {
			return {
				id: i,
				exploded: false,
				style: `
				--x-origin: ${xOrigin}px;
				--y-origin: ${yOrigin}px;
				--x-translate: ${randomBetween(xDomain[0], xDomain[1])}px;
				--y-translate: ${randomBetween(yDomain[0], yDomain[1])}px;
				--animation-delay: ${randomBetween(0, 0.2)}s;
				--animation-duration: ${randomBetween(animationDuaration[0], animationDuaration[1])}s;
				--rotation: ${randomBetween(-360, 360)}deg;
				--animation-fill: ${displace ? 'none' : 'forwards'};
				--dissapear: ${vanish ? '0' : '1'};
   				`
			};
		});

	const clusterBombs = (id: number, event: MouseEvent) => {
		confettis = confettis.map((c) => {
			if (c.id === id) {
				return { ...c, exploded: true }; // Spread the confetti object and set exploded to true
			}
			return c; // Return the confetti as is for those that don't match the id
		});
		confettis = [...confettis];
		removeConfetti(id);
	};

	//HMMM What if we just dont remove the confetti. Lets make a mess !
	const removeConfetti = (id: number) => {
		// setTimeout(() => {
		// 	confettis = confettis.filter((c) => c.id !== id);
		// 	confettis = [...confettis];
		// }, 4000);
	};
</script>

<div class="confetti-container" style="overflow:{showOverflow ? 'visible' : 'hidden'}">
	{#each confettis as c}
		<button style={c.style} class="confetti" on:click={(event) => clusterBombs(c.id, event)}>
			{#if !c.exploded}
				<svg class="heart-svg" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512">
					<!--!Font Awesome Free 6.5.1 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.-->
					<path
						fill={getColor()}
						d="M47.6 300.4L228.3 469.1c7.5 7 17.4 10.9 27.7 10.9s20.2-3.9 27.7-10.9L464.4 300.4c30.4-28.3 47.6-68 47.6-109.5v-5.8c0-69.9-50.5-129.5-119.4-141C347 36.5 300.6 51.4 
			268 84L256 96 244 84c-32.6-32.6-79-47.5-124.6-39.9C50.5 55.6 0 115.2 0 185.1v5.8c0 41.5 17.2 81.2 47.6 109.5z"
					/>
				</svg>
			{:else if clusterBomb === true}
				<Confetti
					clusterBomb={true}
					showOverflow={true}
					animationDuaration={[1, 2]}
					xDomain={[-100, 100]}
					yDomain={[-100, 100]}
					xOrigin={0}
					yOrigin={0}
					confettiAmmount={5}
					vanish={false}
					displace={false}
					colors={['#3772ff', '#e63946', '#c77dff', '#3a86ff', '#8ac926']}
				/>
			{/if}
		</button>
	{/each}
</div>

<style>
	.confetti-container {
		position: absolute;
		pointer-events: none;
		left: 0;
		top: 0;
		width: 100%;
		height: 100%;
	}

	.heart-svg {
		width: 10px;
		height: auto;
	}

	.confetti {
		pointer-events: all;
		left: var(--x-origin);
		top: var(--y-origin);
		position: absolute;
		width: fit-content;
		height: auto;
		border: none;
		background-color: transparent;
		animation: explosion var(--animation-duration) ease-out var(--animation-delay) 1 normal
			var(--animation-fill);
	}

	@keyframes explosion {
		to {
			transform: translate(var(--x-translate), var(--y-translate)) rotate(var(--rotation));
			opacity: var(--dissapear);
		}
	}
</style>
