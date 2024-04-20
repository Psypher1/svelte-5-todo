<script>
	// let todo = [] svelte 4
	let todos = $state([
		{ text: "learn svelte", done: false },
		{ text: "learn turso", done: true },
		{ text: "learn sveltekit", done: false }
	]);
</script>
