<script>
	let { id, title, completed = $bindable(), deleteItem } = $props();

	// Function to handle checkbox change
	function checkboxChanged(event) {
		completed = event.target.checked;
		console.log(`Todo item ${id} updated: ${completed}`);
	}
</script>

<div class="todo-item {completed ? 'completed' : ''}">
	<input type="checkbox" id="item{id}" onchange={checkboxChanged} checked={completed}/>
	<label for="item{id}">{title} ({id})</label>
	<button onclick={() => deleteItem(id)}>Delete</button>
</div>

<style>
	.todo-item {
		display: flex;
		align-items: center;
		margin-bottom: 10px;
		border: 1px solid #ccc;
		padding: 10px;
		border-radius: 5px;
	}

	input[type='checkbox'] {
		margin-right: 10px;
	}

	label {
		flex-grow: 1;
	}

    .completed {
        text-decoration: line-through;
        color: gray;
    }
</style>
