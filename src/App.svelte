<script>
	import { onMount } from 'svelte';

	let todos = []
	let todoText = ''

	onMount(() => {
		todos = JSON.parse(localStorage.getItem('todos'))
	})

	function addTodo(){
		todos = [...todos, todoText]
		localStorage.setItem('todos', JSON.stringify(todos))
	}
</script>

<main>
	<h1>Todo List</h1>
	<form on:submit|preventDefault={addTodo}>
		<input bind:value={todoText} type="text" id="todo-text" placeholder="Enter a todo">
		<button type="submit" id="add-todo">Add Todo</button>
	</form>
	<ul>
		{#each todos as todo}
			<li>{todo}</li>
		{/each}
	</ul>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>