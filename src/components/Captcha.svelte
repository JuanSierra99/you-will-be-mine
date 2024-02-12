<script>
	export let modal_visibility = false;
</script>

<div class="modal">
	<img class="modal-image" src="./crowd_of_people.webp" alt="crowd of people" />
	<p class="prove-text">Prove you aren't a robot</p>
	<div class="select-number-section">
		<p class="prove-text">How many people are in this photo 🤨:</p>
		<input type="number" />
		<button>enter</button>
	</div>
	<button
		on:click={() => {
			modal_visibility = !modal_visibility;
		}}
		class="modal-back-button">back</button
	>
</div>

<style>
	.prove-text {
		text-align: center;
		color: white;
	}

	.select-number-section {
		display: flex;
		justify-content: center;
		flex-direction: row;
	}

	.modal {
		border-radius: 1rem;
		padding: 1em 1em 1em 1em;
		display: flex;
		justify-content: center;
		flex-direction: column;
		z-index: 1000;
		overflow: hidden;
		top: 0;
		left: 1/2;
		right: 1/2;
		transform: translateX(-50%);
		position: absolute;
		width: fit-content;
		height: fit-content;
		background-color: rgb(248, 66, 66);
	}

	.modal-back-button {
		width: fit-content;
	}

	.modal-image {
		border-radius: 1rem;
		margin-left: auto;
		margin-right: auto;
		width: 100%;
		height: auto;
	}
</style>
