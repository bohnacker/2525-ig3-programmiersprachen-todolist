<script>
	let todoList = $state([
		{
			title: 'Learn Svelte',
			completed: false
		},
		{
			title: 'Build a Svelte app',
			completed: false
		},
		{
			title: 'Deploy the app',
			completed: false
		}
	]);

	let inputField;
	let inputValue = $state('');

	function addItem() {
		if (inputValue != '') {
			todoList.push({
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
		<div class="todo-item">
			<input type="checkbox" id="item{i}" />
			<label for="item{i}">{todo.title}</label>
		</div>
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

	.todo-list {
		display: flex;
		flex-direction: column;
	}
	.todo-item {
		display: flex;
		align-items: center;
		margin-bottom: 10px;
	}
	input[type='checkbox'] {
		margin: 0 10px 0 0;
		width: 1.5em;
		height: 1.5em;
		background: white;
		border-radius: 2px;
		border: 1px solid #555;
	}
	/* input[type='checkbox']:checked {
		background: #abd;
	} */
</style>
