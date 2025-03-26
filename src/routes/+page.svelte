<script>
	let todoList = $state(['Erstes Todo', 'Zweites Todo', 'Drittes Todo']);

	let inputValue = $state('');

	function addItem() {
		if (inputValue != '') {
			todoList.push(inputValue);
			inputValue = '';
		}
	}

	function keyPressed(event) {
		if (event.key === 'Enter') {
			addItem();
		}
	}
</script>

<div class="header">
	<input onkeypress={keyPressed} id="todo-input" type="text" bind:value={inputValue} />
	<button onclick={addItem} id="add-button" disabled={inputValue === ""}>Add</button>
</div>

<div class="todo-list">
	{#each todoList as todo, i}
		<div class="todo-item">
			<input type="checkbox" id="item{i}" />
			<label for="item{i}">{todo}</label>
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
</style>
