<script lang="ts">
	import Todo from './components/Todo.svelte'

	let todos: { task: string, done: boolean, id: string }[] = []

	let currentTodo = ''

	function addTodo() {
		todos = [...todos, { task: currentTodo, done: false, id: `${Math.random()}` }]
		currentTodo = ''
	}

	function setDone(id: string, done: boolean) {
		todos = todos.map(todo => todo.id === id ? { ...todo, done } : todo)
	}

	function remove(id: string) {
		todos = todos.filter(todo => todo.id !== id)
	}
</script>

<main>
	<h1>To-do list</h1>
	<input bind:value={currentTodo} />
	<button on:click={addTodo}>Add todo</button>

	<div class="todo-list">
		{#each todos as todo (todo.id)}
			<Todo
				todo={todo.task}
				done={todo.done}
				id={todo.id}
				onSetDone={setDone}
				onRemove={remove}
			/>
		{/each}
	</div>
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

	.todo-list {
		display: flex;
		flex-direction: column;
		gap: .5rem;
	}
</style>