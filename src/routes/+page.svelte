<script>
	import RetroButton from '../components/RetroButton.svelte';
	import RetroText from '../components/RetroText.svelte';
</script>

<div class="retro-container">
	<RetroText text={'YOU WILL'} />
	<RetroText text={'BE MY'} />
	<RetroText text={'VALENTINE'} />
	<div class="retro-buttons">
		<RetroButton text={'YES'} showCaptcha={false} />
		<RetroButton text={'NO'} showCaptcha={true} />
	</div>
</div>

<div class="page-grid">
	<div class="section2">
		<div class="background-hearts">
			<img src="./hearts/kiss-me.svg" class="kiss-me-heart1" alt="..." />
			<img src="./hearts/kiss-me.svg" class="kiss-me-heart2" alt="..." />
			<img src="./hearts/kiss-me.svg" class="kiss-me-heart3" alt="..." />
			<img src="./hearts/xoxo.svg" class="xoxo-heart1" alt="..." />
			<img src="./hearts/xoxo.svg" class="xoxo-heart2" alt="..." />
			<img src="./hearts/xoxo.svg" class="xoxo-heart3" alt="..." />
			<img src="./hearts/my-love.svg" class="my-love-heart1" alt="..." />
			<img src="./hearts/my-love.svg" class="my-love-heart2" alt="..." />
			<img src="./hearts/my-love.svg" class="my-love-heart3" alt="..." />
			<img src="./hearts/i-love-you.svg" class="i-love-you-heart1" alt="..." />
			<img src="./hearts/i-love-you.svg" class="i-love-you-heart2" alt="..." />
			<img src="./hearts/i-love-you.svg" class="i-love-you-heart3" alt="..." />
			<div class="buttons"></div>
			<!-- <img src="./cloud.png" class="cloud-left" alt="..." /> -->
		</div>
	</div>
</div>

<style>
	:global(body) {
		z-index: -9999;
		background-color: #ffe5ec;
	}

	.page-grid {
		display: grid;
		grid-template-rows: repeat(2, 100vh);
	}

	.retro-container {
		z-index: 100;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		width: 100%;
		height: 100%;
		position: fixed;
		animation: anime 1s ease-in-out 1 normal;
		animation-timeline: scroll();
	}

	.retro-buttons {
		opacity: 0;
		animation: appear 10s linear none 1 normal;
		animation-timeline: scroll();
	}

	@keyframes appear {
		from {
			opacity: 0;
		}
		to {
			opacity: 1;
		}
	}

	.background-hearts {
		z-index: 0;
		display: grid;
		position: absolute;
		height: 100%;
		width: 100%;
		grid-template: repeat(10, 1fr) / repeat(10, 1fr);
	}

	.section2 {
		grid-row: 2;
	}

	.kiss-me-heart1,
	.xoxo-heart1,
	.my-love-heart1,
	.kiss-me-heart3,
	.xoxo-heart3,
	.my-love-heart3,
	.i-love-you-heart3 {
		height: 2em;
		animation: distant-animation 5s linear none 1 normal;
		animation-timeline: scroll();
	}

	@keyframes distant-animation {
		from {
			/* opacity: 0 */
			transform: translateY(15rem);
		}
		to {
			/* opacity: 1; */
			transform: translateY(0rem);
		}
	}

	.kiss-me-heart2,
	.xoxo-heart2,
	.my-love-heart2,
	.i-love-you-heart1,
	.i-love-you-heart2 {
		height: 4em;
		animation: closer-animation 5s linear none 1 normal;
		animation-timeline: scroll();
	}

	@keyframes closer-animation {
		from {
			/* opacity: 0 */
			transform: translateY(50rem);
		}
		to {
			/* opacity: 1; */
			transform: translateY(0rem);
		}
	}

	.kiss-me-heart1 {
		grid-row: 9;
		grid-column: 9;
	}

	.kiss-me-heart2 {
		grid-row: 7;
		grid-column: 3;
	}

	.kiss-me-heart3 {
		grid-row: 3;
		grid-column: 6;
	}

	.xoxo-heart1 {
		grid-row: 7;
		grid-column: 8;
	}

	.xoxo-heart2 {
		grid-row: 2;
		grid-column: 7;
	}

	.xoxo-heart3 {
		grid-row: 8;
		grid-column: 2;
	}

	.my-love-heart1 {
		grid-row: 10;
		grid-column: 6;
	}

	.my-love-heart2 {
		grid-row: 5;
		grid-column: 9;
	}

	.my-love-heart3 {
		grid-row: 3;
		grid-column: 3;
	}

	.i-love-you-heart1 {
		grid-row: 2;
		grid-column: 2;
	}

	.i-love-you-heart2 {
		grid-row: 10;
		grid-column: 7;
	}

	.i-love-you-heart3 {
		grid-row: 3;
		grid-column: 9;
	}
</style>
