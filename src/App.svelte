<script>
	import { onMount } from "svelte";
	const API = "https://rickandmortyapi.com/api/character";
	let data = [];
	let characters = [];
	onMount(async () => {
		const response = await fetch(API)
		data = await response.json()
		characters = data.results
	});
</script>

<style>
	.characters {
		width: 100%;
		display: grid;
		grid-template-columns: repeat(5, 1fr);
		grid-gap: 8px
	}
	figure img {
		width: 100%;
		margin: 0;
		filter: grayscale(100%)
	}
	/* .loading {
		background-color: aqua;
		width: 100px;
		height: 100px;
		animation-name: coloranimate;
		animation-duration: 4s;
	}

	@keyframes coloranimate {
		from {
			background-color: red;
		}
		to {
			background-color: black;
		}
	} */

	.loading {
		width: 100px;
		height: 100px;
		background-color: black;
		border-radius: 50%;
		border: 20px solid red;
		border-top: 20px solid white;
		animation: loader 2s liner infinite;
	}

	@keyframes loader {
		0% {
			transform: rotate(0deg);
		}
		100% {
			transform: rotate(360deg);
		}
	}
</style>

<div class="Loading" />
<div class="characters">
	{#each characters as character}
		<figure>
			<img src="{character.image}" alt="{character.name}">
			<figcaption>{character.name}</figcaption>
		</figure>
	{:else}
		<div class="Loading" />
	{/each}
</div>