<script>
	// let todos =  svelte 4
	// $: todos = []

	let todos = $state([
		{ text: "learn svelte", done: false },
		{ text: "learn turso", done: true },
		{ text: "learn sveltekit", done: false }
	]);

	function addTodo(event) {
		if (event.key !== "Enter") return;

		const todoEl = event.target;
		// const id = window.crypto.randomUUID()
		const text = todoEl.value;
		const done = false;

		todos = [...todos, { text, done }];

		todoEl.value = "";
	}
</script>

<svelte:head>
	<title>Svelte 5 Todo</title>
</svelte:head>

<h1>A Todo Thing</h1>

<!-- <input on:keydown={} type="text" placeholder="Add todo" /> -->
<!-- event listeners are now attributes -->
<input on:keydown={addTodo} type="text" placeholder="Add todo" />

<div class="todos">
	{#each todos as todo}
		<div class="todo">
			<input type="text" name="" value={todo.text} id="" />
			<input type="checkbox" name="" checked={todo.done} id="" />
		</div>
	{/each}
</div>

<style>
	h1 {
		font-size: var(--size-fluid-4);
		margin-bottom: var(--size-7);
	}
	/* input {
		padding: var(--size-3);
		background-color: var(--gray-8);
		color: var(--gray-2);
		margin-bottom: var(--size-3);
		border: none;
	} */

	input[type="text"] {
		width: 100%;
		padding: 1rem;
		background-color: var(--gray-9);
	}

	input[type="checkbox"] {
		position: absolute;
		right: 4%;
		top: 50%;
		translate: 0% -50%;
	}

	.todos {
		display: grid;
		gap: 1rem;
		margin-block-start: 1rem;
	}

	.todo {
		position: relative;
		transition: opacity 0.3s;
	}

	.completed {
		opacity: 0.4;
	}
</style>
