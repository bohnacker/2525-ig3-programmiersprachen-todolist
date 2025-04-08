<script>
	let { todo, i } = $props();
</script>

<div class="todo-item">
	<input type="checkbox" id="item{i}" />
	<label for="item{i}">{todo}</label>
</div>
