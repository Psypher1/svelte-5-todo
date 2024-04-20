<script>
	/** @type {import('./$types').LayoutData} */

	import "../app.css";
</script>

<main>
	<slot />
</main>

<style>
	main {
		padding: var(--size-12);
		display: grid;
		place-items: center;
		max-width: 70ch;
	}
</style>
