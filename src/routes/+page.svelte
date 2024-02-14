<script lang="ts">
	import RetroButton from '../components/RetroButton.svelte';
	import RetroText from '../components/RetroText.svelte';
	export const mainText = ['YOU WILL', 'BE MY', 'VALENTINE'];
	import Confetti from '../components/Confetti.svelte';
	import Captcha from '../components/Captcha.svelte';
	let yes_button_clicked = false;
	let no_button_clicked = false;
</script>

<div class="retro-container">
	{#each mainText as txt}
		<RetroText text={txt} />
	{/each}

	<div class="retro-buttons">
		<RetroButton
			text={'YES'}
			buttonClickFunction={() => {
				yes_button_clicked = !yes_button_clicked;
			}}
		/>
		<RetroButton
			text={'NO'}
			buttonClickFunction={() => {
				no_button_clicked = !no_button_clicked;
			}}
		/>
		{#if yes_button_clicked}
			<div class="contain">
				<Confetti
					clusterBomb={true}
					animationDuaration={[1, 5]}
					xDomain={[-window.innerWidth / 2, window.innerWidth / 2]}
					yDomain={[0, screen.height]}
					xOrigin={window.innerWidth / 2}
					yOrigin={0}
					confettiAmmount={100}
					displace={false}
				/>
			</div>
		{/if}
		{#if no_button_clicked}
			<Captcha></Captcha>
		{/if}
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
		</div>
	</div>
</div>

<style>
	.contain {
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		position: absolute;
		pointer-events: none;
		/* background-color: green; */
	}

	:global(body) {
		z-index: -9999;
		background-color: #ffe5ec;
		padding: 1;
		margin: 0;
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
