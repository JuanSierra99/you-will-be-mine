<script lang="ts">
	export let text: string;
</script>

<div class="text-container">
	<h1 class="retro-text">{text}</h1>
</div>

<style>
	.text-container {
		font-family: 'retro';
		background-color: transparent;
		width: 100%;
		height: fit-content;
	}

	.retro-text {
		font-size: 4rem;
		text-align: center;
		margin: 0;
		color: #f7265a;
		text-shadow: 4px 3px 0px #ffa1e1;
	}

	:global(body.dark-mode) .retro-text {
		color: #f7265a;
	}

	@font-face {
		font-family: 'retro';
		src: url('/fonts/BambiRetro-WyjGG.ttf');
	}
</style>
