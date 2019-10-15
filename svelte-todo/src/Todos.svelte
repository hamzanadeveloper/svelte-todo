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
$: filteredTodos = currentFilter === 'all' ? todos.sort(function(a,b){return a.completed-b.completed})
    : currentFilter === 'completed'
    ? todos.filter(todo => todo.completed)
    : todos.filter(todo => !todo.completed)

function checkAllTodos(event) {
    todos.forEach(todo => todo.completed = event.target.checked);
    todos = todos;
}

function updateFilter(newFilter) {
    currentFilter = newFilter;
}

function clearCompleted() {
    todos = todos.filter(todo => !todo.completed);
}

function handleDeleteTodo(event) {
    todos = todos.filter(todo => todo.id !== event.detail.id);
}
function handleToggleComplete(event) {
    const todoIndex = todos.findIndex(todo => todo.id === event.detail.id);
    const updatedTodo = { ...todos[todoIndex], completed: !todos[todoIndex].completed};
    todos = [
        ...todos.slice(0, todoIndex),
        updatedTodo,
        ...todos.slice(todoIndex + 1),
    ];
}

</script>

<div class="container">
    <div class="title">SVELTE NOTES</div>

    <input type="text" class="todo-input" placeholder="New note..." bind:value={newTodoTitle} on:keydown={addTodo}>

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

<style>
    .title{
        font-family: 'Fjalla One', sans-serif;
            text-align: center;
            font-size: 39px;
            font-style: italic;

    }
    .container {
        max-width: 600px;
        border: 1px solid #888;
        margin: 10px auto;
        padding: 15px;
        border-radius: 10px;
    }
    .logo {
        display: block;
        margin: 20px auto;
        width: 50%;
    }
    .todo-input {
        width: 100%;
        padding: 10px, 20px;
        font-size: 18px;
        border-radius: 9px;
        outline: none;
        margin-bottom: 20px;
    }
    .todo-input {
            width: 100%;
            padding: 10px, 20px;
            font-size: 18px;
            border-radius: 9px;
            outline: none;
            margin-bottom: 20px;
    }
    .todo-input:focus{
    border: 1px solid #02b44b;
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
    button {
        font-size: 14px;
        background-color: white;
        appearance: none;
    }
    button:hover {
        background: lightseagreen;
    }
    button:focus {
        outline: none;
    }
    .active {
        background: lightseagreen;
    }
</style>
