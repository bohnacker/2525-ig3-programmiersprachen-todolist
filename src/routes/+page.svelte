<script>
	import ListItem from '$lib/ListItem.svelte';

	let todoList = $state([
		{ id: 1, title: 'Erstes Todo', completed: false },
		{ id: 2, title: 'Zweites Todo', completed: false },
		{ id: 4, title: 'Drittes Todo', completed: false }
	]);
	// initialize nextID to the highest id in the todoList + 1
	let nextID = $state(
		todoList.length > 0 ? Math.max(...todoList.map(todo => todo.id)) + 1 : 1
	);

	let inputValue = $state('');

	let sortedTodoList = $derived(
		todoList.sort((a, b) => {
			if (a.completed === b.completed) {
				return a.id - b.id;
			}
			return a.completed ? 1 : -1;
		})
	);

	function addItem() {
		if (inputValue != '') {
			todoList.push({ id: nextID++, title: inputValue, completed: false });
			inputValue = '';
		}
		console.log(todoList);
	}

	function keyPressed(event) {
		if (event.key === 'Enter') {
			addItem();
		}
	}
</script>

<div class="header">
	<input onkeypress={keyPressed} id="todo-input" type="text" bind:value={inputValue} />
	<button onclick={addItem} id="add-button" disabled={inputValue === ''}>Add</button>
</div>

<div class="todo-list">
	{#each sortedTodoList as todo, i}
		<ListItem id={todo.id} title={todo.title} bind:completed={todo.completed} />
	{/each}
</div>

<style>
	.header {
		display: flex;
		margin-bottom: 20px;
	}
	#todo-input {
		display: flex;
		width: 100%;
		margin-right: 10px;
	}
</style>
