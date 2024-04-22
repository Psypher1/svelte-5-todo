<script>
	/** @type {import('./$types').LayoutData} */

	import "../app.css";
</script>

<main>
	<slot />
</main>

<style>
	main {
		padding: var(--size-10);
		display: grid;
		place-items: center;
		max-width: 90ch;
		margin-inline: auto;
	}
</style>
