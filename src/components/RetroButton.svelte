<script lang="ts">
	export let text: string;
	export let showCapcha: boolean;
	import Confetti from './Confetti.svelte';
	let yes_clicked = false;
	let peopleNumber = 0;
	let modal_visibility = false;
	/*We will show this if the no button is clicked*/
	const changeModalVisibility = () => {
		modal_visibility = !modal_visibility;
	};

	/*do something if they somehow guess the right answer for capcha*/
	const checkNumAnswer = () => {
		if (peopleNumber === 911) {
			return true;
		}
		return false;
	};

	/*pretty much just dark mode but sexy*/
	const setTheMood = () => {
		yes_clicked = !yes_clicked;
		// window.document.body.classList.toggle('dark-mode');
	};
</script>

<button class="retro-button" on:click={showCapcha ? changeModalVisibility : setTheMood}
	>{text}</button
>

{#if modal_visibility && showCapcha}
	<div class="modal">
		<p class="prove-text">prove you are not a robot</p>
		<img class="modal-image" src="./people.jpg" alt="..." />
		<div class="select-number-section">
			<p class="prove-text">How many people are in this photo:</p>
			<input type="number" bind:value={peopleNumber} />
			<button on:click={checkNumAnswer}>enter</button>
		</div>

		<button on:click={changeModalVisibility}>back</button>
	</div>
{/if}

{#if yes_clicked}
	<Confetti xOrigin={500} yOrigin={0} />
{/if}

<style>
	.retro-button {
		height: 3rem;
		padding: 1rem;
		color: white;
		background-color: pink;
		width: 5rem;
		font-family: 'retro';
		border-radius: 1rem;
		border: none;
		box-shadow: 3px 2px 0px red;
	}

	@font-face {
		font-family: 'retro';
		src: url('./RetroText.svelte');
	}

	.retro-button:hover {
		box-shadow: 3px 3px 0px rgb(220, 63, 63);
	}

	.prove-text {
		text-align: center;
		color: black;
	}

	.select-number-section {
		display: flex;
		justify-content: center;
		flex-direction: row;
	}

	.modal {
		display: flex;
		justify-content: center;
		flex-direction: column;
		overflow: hidden;
		z-index: 100;
		top: 0;
		left: 1/2;
		right: 1/2;
		transform: translateX(-50%);
		position: absolute;
		width: fit-content;
		height: fit-content;
		background-color: white;
	}

	.modal-image {
		margin-left: auto;
		margin-right: auto;
		width: 100%;
		height: auto;
	}
</style>
