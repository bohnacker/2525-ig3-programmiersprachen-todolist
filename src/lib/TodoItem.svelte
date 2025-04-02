<script>
	let { id, title, completed } = $props();
</script>

<div class="todo-item">
	<input type="checkbox" id="item{id}" />
	<label for="item{id}">{title} ({id})</label>
</div>

<style>
	.todo-item {
		display: flex;
		align-items: center;
		/* margin-bottom: 10px; */
		border-bottom: 1px solid #0005;
		padding: 10px;
		border-radius: 0px;
		background: #f9f9f9;
	}
	input[type='checkbox'] {
		margin: 0 10px 0 0;
		width: 1.5em;
		height: 1.5em;
		background: white;
		border-radius: 2px;
		border: 1px solid #555;
	}
</style>
