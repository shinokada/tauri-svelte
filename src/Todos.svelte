<script>
  import TodoItem from './TodoItem.svelte'
  import { Input, Button } from 'flowbite-svelte'
  // import Button from './lib/Button.svelte'
  let newTodoTitle = ''
  let currentFilter = 'all'
  let nextId = 4
  let todos = [
    {
      id: 1,
      title: 'My first todo',
      completed: false,
    },
    {
      id: 2,
      title: 'My second todo',
      completed: false,
    },
    {
      id: 3,
      title: 'My third todo',
      completed: false,
    },
  ]
  const addTodo = (event) => {
    if (event.key === 'Enter') {
      todos = [
        ...todos,
        {
          id: nextId,
          completed: false,
          title: newTodoTitle,
        },
      ]
      nextId = nextId + 1
      newTodoTitle = ''
    }
  }
  $: todosRemaining = filteredTodos.filter((todo) => !todo.completed).length
  $: filteredTodos =
    currentFilter === 'all'
      ? todos
      : currentFilter === 'completed'
      ? todos.filter((todo) => todo.completed)
      : todos.filter((todo) => !todo.completed)
  const checkAllTodos = (event) => {
    todos.forEach((todo) => (todo.completed = event.target.checked))
    todos = todos
  }
  const updateFilter = (newFilter) => {
    currentFilter = newFilter
  }
  const clearCompleted = () => {
    todos = todos.filter((todo) => !todo.completed)
  }
  const handleDeleteTodo = (event) => {
    todos = todos.filter((todo) => todo.id !== event.detail.id)
  }
  const handleToggleComplete = (event) => {
    const todoIndex = todos.findIndex((todo) => todo.id === event.detail.id)
    const updatedTodo = { ...todos[todoIndex], completed: !todos[todoIndex].completed }
    todos = [...todos.slice(0, todoIndex), updatedTodo, ...todos.slice(todoIndex + 1)]
  }
</script>

<div class="container">
  <h2>Svelte Todo App</h2>
  <input
    type="text"
    class="todo-input"
    placeholder="Insert todo item ..."
    bind:value={newTodoTitle}
    on:keydown={addTodo}
  />

  {#each filteredTodos as todo}
    <div class="todo-item">
      <TodoItem
        {...todo}
        on:deleteTodo={handleDeleteTodo}
        on:toggleComplete={handleToggleComplete}
      />
    </div>
  {/each}

  <div class="inner-container">
    <div>
      <label
        ><input class="inner-container-input" type="checkbox" on:change={checkAllTodos} />Check All</label
      >
    </div>
    <div>{todosRemaining} items left</div>
  </div>

  <div class="inner-container">
    <div>
      <Button
        on:click={() => updateFilter('all')}
        class={currentFilter === 'all' ? 'bg-green-500' : ''}>All</Button
      >
      <Button
        on:click={() => updateFilter('active')}
        class={currentFilter === 'active' ? 'bg-green-500' : ''}>Active</Button
      >
      <Button
        on:click={() => updateFilter('completed')}
        class={currentFilter === 'completed' ? 'bg-green-500' : ''}>Completed</Button
      >
    </div>
    <dir>
      <Button on:click={clearCompleted}>Clear Completed</Button>
    </dir>
  </div>
</div>

<style>
  .container {
    max-width: 800px;
    margin: 10px auto;
  }

  .todo-input {
    width: 100%;
    padding: 10px, 20px;
    font-size: 18px;
    margin-bottom: 20px;
  }
  .inner-container {
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-size: 16px;
    border-top: 1px solid lightgrey;
    padding-top: 15px;
    margin-bottom: 13px;
  }
  .inner-container-input {
    margin-right: 12px;
  }
</style>
