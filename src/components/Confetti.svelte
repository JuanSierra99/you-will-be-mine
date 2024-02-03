<script lang="ts">
	import { slide } from 'svelte/transition';
	const randomizeAnimation = () => {
		const duration = Math.random() * 10 + 2;
		const delay = Math.random() * 3;
		return 'explosion 1s';
	};

	const randomSize = () => {
		return `${Math.random() * 8 + 2}px`;
	};

	const randomColor = () => {
		const colors = ['white', 'black'];
		const random = colors[Math.floor(Math.random() * colors.length)];
		return random;
	};
</script>

{#each Array(50) as _, i}
	<span
		class="confetti"
		style="transform: translateX(--var{Math.random() *
			screen.availWidth}px); width: {randomSize()}; height:{randomSize()}; background-color: {randomColor()}"
	></span>
{/each}

<style>
	.confetti {
		left: 0;
		top: 0;
		position: absolute;
		width: 10px;
		height: 10px;
		background-color: lightblue;
		animation: explosion 2s;
	}

	@keyframes explosion {
		from {
			transform: translateX(0);
			transform: translateY(0);
		}
		to {
			transform: translateX(0);
			transform: translateY(100px);
		}
	}
</style>
