<script>
import TodoItem from './TodoItem.svelte';

let todos = [
    {
        id: 1,
        title: 'My first todo',
        completed: false
    },
    {
        id: 2,
        title: 'My second todo',
        completed: false
    },
    {
        id: 3,
        title: 'My third todo',
        completed: false
    },
];

let newTodoTitle ='';
let currentFilter = 'all';
let nextId = 4;

function addTodo(event) {
    if (event.key === 'Enter') {
        todos = [...todos, {
            id: nextId,
            completed: false,
            title: newTodoTitle
        }];
        nextId = nextId + 1;
        newTodoTitle = '';
    }
}

$: todosRemaining = filteredTodos.filter(todo => !todo.completed).length;
$: filteredTodos = currentFilter === 'all' ? todos : currentFilter === 'completed'
    ? todos.filter(todo => todo.completed)
    : todos.filter(todo => !todo.completed)

function checkAllTodos(event) {
    todos.forEach(todo => todo.completed = event.target.checked);
    todos = todos;
}

function updateFilter(newFilter) {
    currentFilter = newFilter;
}

</script>

<div class="container">
    <h2>Svelte Todo App

    <input type="text" class="todo-input" placeholder="Insert todo item ..." bind:value={newTodoTitle} on:keydown={addTodo}>

    {#each filteredTodos as todo}
        <div class="todo-item">
            <TodoItem {...todo} on:deleteTodo={handleDeleteTodo} on:toggleComplete={handleToggleComplete} />
        </div>
    {/each}

    <div class="inner-container">
        <div><label><input class="inner-container-input" type="checkbox" on:change={checkAllTodos}>Check All</label></div>
        <div>{todosRemaining} items left</div>
    </div>

    <div class="inner-container">
        <div>
            <button on:click={() => updateFilter('all')} class:active="{currentFilter === 'all'}">All</button>
            <button on:click={() => updateFilter('active')} class:active="{currentFilter === 'active'}">Active</button>
            <button on:click={() => updateFilter('completed')} class:active="{currentFilter === 'completed'}">Completed</button>
        </div>
        <div>
            <button on:click={clearCompleted}>Clear Completed</button>
        </div>
    </div>

</div>