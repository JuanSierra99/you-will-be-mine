<script lang="ts">
	export let text: string;
	export let buttonClickFunction;
</script>

<button class="retro-button" on:click={buttonClickFunction}>{text}</button>

<style>
	/*The container that will hold all the confetti */

	.retro-button {
		height: 3rem;
		padding: 1rem 2rem 1rem 2rem;
		margin: 1rem;
		color: white;
		background-color: #ffc8dd;
		width: fit-content;
		font-family: 'retro';
		border-radius: 1rem;
		border: none;
		box-shadow: 3px 2px 0px #e63946;
	}

	@font-face {
		font-family: 'retro';
		src: url('./RetroText.svelte');
	}

	.retro-button:hover {
		background-color: #ffafcc;
		box-shadow: 4px 3px 0px #e63946;
	}
</style>
