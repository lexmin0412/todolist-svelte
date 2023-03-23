<script lang="ts">
	import TodoItem from "./components/todo-item.svelte";

	let newTodoText = ''
	let list = JSON.parse(localStorage.getItem('todo-list') || '[]')
	const handleAdd = () => {
		console.log('newTodoText', newTodoText)
		list = [...list,  {
			id: (list.length + 1).toString(),
			title: newTodoText
		}]
		newTodoText = ''
	}

	// 监听 list 变化，存储到 localstorage 中
	$: localStorage.setItem('todo-list', JSON.stringify(list))
</script>

<div>
	<input type="text" bind:value={newTodoText} />
	<button on:click={handleAdd}>add</button>
</div>

{#each list as item, index}
	<TodoItem title={item.title} index={index+1} />
{/each}


