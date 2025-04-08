<script>
	let { id, title, completed = $bindable() } = $props();

	// Function to handle checkbox change
	function checkboxChanged(event) {
		completed = event.target.checked;
		console.log(`Todo item ${id} updated: ${completed}`);
	}
</script>

<div class="todo-item {completed ? 'completed' : ''}">
	<input type="checkbox" id="item{id}" onchange={checkboxChanged} />
	<label for="item{id}">{title} ({id})</label>
</div>

<style>
	.todo-item {
		display: flex;
		align-items: center;
		margin-bottom: 10px;
	}

	input[type='checkbox'] {
		margin-right: 10px;
	}

    .completed {
        text-decoration: line-through;
        color: gray;
    }
</style>
