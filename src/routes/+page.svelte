<script>
	// let todos =  svelte 4
	// $: todos = []

	let todos = $state([
		// { text: "learn svelte", done: false },
		// { text: "learn turso", done: true },
		// { text: "learn sveltekit", done: false }
	]);

	let filter = $state("all");
	let filteredTodos = $derived(filterTodos());

	// $: console.log(todos)

	/* an effect is a signal that reruns every time a change occurs */
	// $effect(() => {
	// 	console.log(todos);
	// 	console.log(filter);
	// });

	// check todos in storage
	$effect(() => {
		const savedTodos = localStorage.getItem("todos");
		savedTodos && (todos = JSON.parse(savedTodos));

		// if (savedTodos){
		// 	todos = JSON.parse(savedTodos)
		// }
	});

	// add todod
	$effect(() => {
		localStorage.setItem("todos", JSON.stringify(todos));
	});

	function addTodo(event) {
		if (event.key !== "Enter") return;

		const todoEl = event.target;
		// const id = window.crypto.randomUUID()
		const text = todoEl.value;
		const done = false;

		todos = [...todos, { text, done }];

		todoEl.value = "";
	}

	function editTodo(event) {
		const inputEl = event.target;
		const index = inputEl.dataset.index;

		todos[index].text = inputEl.value;
	}

	function toggleTodo(event) {
		const inputEl = event.target;
		const index = inputEl.dataset.index;

		todos[index].done = !todos[index].done;
	}

	function deleteTodo(index) {
		// todos = todos.filter((todo) => todo.index !== index);
		const inputEl = event.target;
		const index = inputEl.dataset.index;

		todos = todos.filter((todo) => todo[index] !== todo[index]);
	}

	function setFilter(newFilter) {
		filter = newFilter;
	}

	function filterTodos() {
		// if you return in switch, no need for break
		switch (filter) {
			case "all":
				return todos;
			case "active":
				return todos.filter((todo) => !todo.done);
			case "completed":
				return todos.filter((todo) => todo.done);
			default:
				break;
		}
	}

	function remaining() {
		return todos.filter((todo) => !todo.done).length;
	}
</script>

<svelte:head>
	<title>Svelte 5 Todo</title>
</svelte:head>

<h1>A Todo Thing</h1>

<!-- <input on:keydown={} type="text" placeholder="Add todo" /> -->
<!-- event listeners are now attributes -->
<input on:keydown={addTodo} type="text" placeholder="Add todo" class="add-todo" />

<div class="todos">
	{#each filteredTodos as todo, i}
		<div class="todo" class:completed={todo.done}>
			<input type="text" oninput={editTodo} data-index={i} name="" value={todo.text} id="" />
			<input type="checkbox" onchange={toggleTodo} data-index={i} checked={todo.done} id="" />
			<button on:click={deleteTodo}>X</button>
		</div>
	{/each}
</div>

<div class="filters">
	<button on:click={() => setFilter("all")}>All</button>
	<button on:click={() => setFilter("active")}>Active</button>
	<button on:click={() => setFilter("completed")}>Completed</button>
</div>

<p>{remaining()} remaining</p>

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
		right: 10%;
		top: 50%;
		translate: 0% -50%;
	}

	.todos {
		display: grid;
		gap: 1rem;
		margin-block-start: 1rem;

		width: 40ch;
		margin-top: var(--size-5);
	}

	.todo {
		display: flex;
		position: relative;
		transition: opacity 0.3s;
	}
	.todo > button {
		color: red;
		font-size: var(--font-size-3);

		position: absolute;
		right: -20%;
		top: 44%;
		translate: 0% -50%;

		cursor: pointer;
	}
	.add-todo {
		width: 40ch !important;
	}

	.filters {
		margin-block: var(--size-5);
	}

	.completed {
		opacity: 0.4;
	}
</style>
