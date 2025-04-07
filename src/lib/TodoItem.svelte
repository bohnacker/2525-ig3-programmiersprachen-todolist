<script>
	// import trash icon
	import { Icon } from 'svelte-icons-pack';
	import { OiTrash16 } from "svelte-icons-pack/oi";
	import { FiTrash } from "svelte-icons-pack/fi"; 

	let { id, title, completed = $bindable(), deleteItem } = $props();

	function updateState(event) {
		completed = event.target.checked;
		// console.log('Updated state for id ' + id + ' to ' +  completed);
	}
</script>

<div class={['todo-item', { completed }]}>
	
	<input type="checkbox" id="item{id}" onchange={updateState} checked={completed} />
	<label for="item{id}">{title} ({id})</label>
	<!-- add trash button -->
	<button
		class="delete-button"
		onclick={() => {deleteItem(id)}}><Icon src={OiTrash16} size="16"/></button
	>
	
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
	.todo-item.completed {
		background: #f0f0f0;
		text-decoration: line-through;
		opacity: 0.5;
	}
	input[type='checkbox'] {
		margin: 0 10px 0 0;
		width: 1.5em;
		height: 1.5em;
		background: white;
		border-radius: 2px;
		border: 1px solid #555;
	}
	.delete-button {
		margin-left: auto;
		background: #ff000000;
		color: red;
		border: none;
		padding: 7px 7px;
		border-radius: 5px;
		cursor: pointer;
		text-decoration: none;
	}
	.delete-button:hover {
		background: #ff0000;
		color: white;
	}
	.delete-button:active {
		background: #ff0000;
		color: white;
	}
	.delete-button:focus {
		outline: none;
	}
	.delete-button:focus-visible {
		outline: 2px solid #0005;
	}
</style>
