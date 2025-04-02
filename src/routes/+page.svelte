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
	// get highest id in the list
	let nextId = Math.max(...todoList.map((todo) => todo.id)) + 1;
	// if list is empty, set nextId to 1
	if (isNaN(nextId)) {
		nextId = 1;
	}

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
	<button onclick={addItem} id="add-button" disabled={inputValue === ''}>Add</button>
</div>

<div class="todo-list">
	{#each todoList as todo, i}
		<TodoItem {...todo} />
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
	}

</style>
