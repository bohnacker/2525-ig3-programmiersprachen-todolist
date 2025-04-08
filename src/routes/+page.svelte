<script>
	import TodoItem from '$lib/TodoItem.svelte';

	let todoList = $state([
		{
			id: 1,
			title: 'Learn Svelte',
			completed: false
		},
		{
			id: 2,
			title: 'Build a Svelte app',
			completed: false
		},
		{
			id: 3,
			title: 'Deploy the app',
			completed: false
		}
	]);
	// get highest id in the list to use as nextId
	let nextId = Math.max(...todoList.map((todo) => todo.id)) + 1;
	// if list is empty, set nextId to 1
	if (isNaN(nextId)) {
		nextId = 1;
	}

	$inspect(todoList);

	let openTodos = $derived(todoList.filter((todo) => !todo.completed));
	let completedTodos = $derived(todoList.filter((todo) => todo.completed));

	let inputField;
	let inputValue = $state('');

	function addItem() {
		if (inputValue != '') {
			todoList.push({
				id: nextId++,
				title: inputValue,
				completed: false
			});
			inputValue = '';
		}
		// Focus input field
		inputField.focus();
	}

	function keyPressed(event) {
		if (event.key === 'Enter') {
			addItem();
		}
	}

	function deleteItem(id) {
		todoList = todoList.filter((todo) => todo.id !== id);
	}
</script>

<div class="header">
	<input
		bind:this={inputField}
		onkeypress={keyPressed}
		id="todo-input"
		type="text"
		bind:value={inputValue}
		placeholder="Your new Todo"
	/>
	<!-- use tailwind to style button -->
	<button
		class="bg-blue-500 text-white px-4 py-2 rounded shadow hover:bg-blue-600 transition duration-200 ease-in-out"
		onclick={addItem}
		id="add-button"
		disabled={inputValue === ''}>Add</button
	>
</div>

{#if openTodos.length > 0}
	<div class="todo-list open">
		{#each openTodos as todo, i (todo.id)}
			<TodoItem id={todo.id} title={todo.title} bind:completed={todo.completed} {deleteItem} />
		{/each}
	</div>
{/if}

{#if completedTodos.length > 0}
	<div class="todo-list completed">
		{#each completedTodos as todo, i (todo.id)}
			<TodoItem id={todo.id} title={todo.title} bind:completed={todo.completed} {deleteItem} />
		{/each}
	</div>
{/if}

<style>
	.header {
		display: flex;
		margin-bottom: 20px;
	}

	#todo-input {
		display: flex;
		width: 100%;
		padding: 10px;
		border: 1px solid #0005;
		border-radius: 5px;
		background: #f9f9f9;
		box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
		margin-right: 10px;
	}

	.todo-list {
		display: flex;
		flex-direction: column;
		border: 1px solid #0005;
		border-radius: 5px;
		overflow: hidden;
		box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
		margin-bottom: 20px;
	}
</style>
