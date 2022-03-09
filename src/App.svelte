<script>
	import Login from './Login.svelte';
	export let name;
</script>

<main>
	<h1 class="hero">Travel Packing Checklist</h1>
	
	<Login />
</main>

<style>
	:global(body) {
		background-color: gray;
	}
	

	h1 {
		color: lightgray;
		text-transform: uppercase;
		font-size: 3rem;
		font-weight: 100;
	}

	.hero {
		--height: 7rem;
		background-color: orange;
		color: white;
		height: var(--height);
		line-height: var(--height);
		margin: 0 0 2rem 0;
		text-align: center;
		vertical-align: middle;
		width: 100vw;
	}

	main {
		color: white;
		display: flex;
		flex-direction: column;
		justify-content: flex-start;
		align-items: center;
	}
	/* @media (min-width: 640px) {
		main {
			max-width: none;
		}
	} */
</style>