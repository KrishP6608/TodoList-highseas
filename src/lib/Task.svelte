<script>
	import { createEventDispatcher } from 'svelte';
	const dispatch = createEventDispatcher();

	export let task;
	import { fade, slide } from 'svelte/transition';

	// Update the Task
	function updateTask(updated) {
		task = { ...task, ...updated };
		dispatch('update', task);
	}

	// Add a toggle logic
	function toggle() {
		updateTask({ isDone: task.isDone });
		console.log(task);
	}

	// Remove the Task
	function remove() {
		dispatch('remove', task);
	}

	// Update the name of the Task
	function changeName() {
		updateTask({ name: task.name });
	}

	function handleRemove() {
		dispatch('remove', task);
	}

	function handleUpdate() {
		dispatch('update', task);
	}
</script>

<div class="task" in:slide={{ duration: 300 }} out:slide={{ duration: 300 }}>
	<input type="checkbox" bind:checked={task.isDone} on:change={handleUpdate} />
    <input type="text" bind:value={task.name} on:change={handleUpdate} class:is-done={task.isDone} />
	<button on:click={handleRemove}>Remove</button>
</div>

<!-- Styling the Task-->
<style>
	
	.task {
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding: 0.5rem;
		border-bottom: 1px solid #ddd;
	}

	.task input[type="text"] {
		flex: 1;
		margin: 0 0.5rem;
		padding: 0.5rem;
		border: 1px solid #ddd;
		border-radius: 4px;
	}

	.task input[type="text"].is-done {
        text-decoration: line-through;
        color: gray;
    }

	.task button {
		background-color: #dc3545;
		color: white;
		border: none;
		border-radius: 4px;
		padding: 0.5rem;
		cursor: pointer;
		transition: background-color 0.3s ease;
	}

	.task button:hover {
		background-color: #c82333;
	}
</style>