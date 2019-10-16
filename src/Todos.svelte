<script>
import TodoItem from './TodoItem.svelte';

let todos = [
    {
        id: 1,
        title: 'My first todo',
        completed: false,
        topic: 'general'
    },
    {
        id: 2,
        title: 'My second todo',
        completed: false,
        topic: 'general'
    },
    {
        id: 3,
        title: 'My third todo',
        completed: false,
        topic: 'general'
    },
];

let newTodoTitle ='';
let newTodoTopic ='';
let currentFilter = 'all';
let nextId = 4;
let currentTopic = 'general';


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
function addTopic(event) {
    if (event.key === 'Enter') {
        topics = [ ...topics, newTodoTopic]
        newTodoTopic = ''
    }
}

$: topics = ['general']
$: todosRemaining = filteredTodos.filter(todo => !todo.completed).length;
$: filteredTodos = currentFilter === 'all' ? todos.sort(function(a,b){return a.completed-b.completed})
    : currentFilter === 'completed'
    ? todos.filter(todo => todo.completed)
    : todos.filter(todo => !todo.completed)


function checkAllTodos(event) {
    todos.forEach(todo => todo.completed = event.target.checked);
    todos = todos;
}

function changeTopic(data){
    console.log(data)
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
function capitalizeFirstLetter(string) {
    return string.charAt(0).toUpperCase() + string.slice(1);
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
<div class="page">
    <div class="topics">
        <div class="title" style="font-size: 24px; padding-bottom: 20px;">NOTE TOPICS</div>

        <input type="text" class="todo-input" placeholder="New topic..." bind:value={newTodoTopic} on:keydown={addTopic}>

        <div class="active-topics">TOPICS</div>

        {#each topics as topic}
            <button class="button-topics" on:click={()=>changeTopic(topic)} >{capitalizeFirstLetter(topic)}</button>
        {/each}
    </div>
    <div class="container">
        <div class="title">SVELTE NOTES</div>

        <input type="text" class="todo-input" placeholder="New note..." bind:value={newTodoTitle} on:keydown={addTodo}>

        {#each filteredTodos as todo}
            <div class="todo-item">
                <TodoItem {...todo} on:deleteTodo={handleDeleteTodo} on:toggleComplete={handleToggleComplete} />
            </div>
        {/each}

        <div class="inner-container">
            <div style="font-family: 'Raleway', sans-serif;"><label><input class="inner-container-input" type="checkbox" on:change={checkAllTodos}>Check All</label></div>
            <div style="font-family: 'Raleway', sans-serif;">{todosRemaining} items left</div>
        </div>

        <div class="inner-container">
            <div>
                <button class="filter-btn" on:click={() => updateFilter('all')} class:active="{currentFilter === 'all'}">ALL</button>
                <button class="filter-btn" on:click={() => updateFilter('active')} class:active="{currentFilter === 'active'}">ACTIVE</button>
                <button class="filter-btn" on:click={() => updateFilter('completed')} class:active="{currentFilter === 'completed'}">COMPLETE</button>
            </div>
            <div>
                <button class="clear-btn" style="width:90px" on:click={clearCompleted}>CLEAR COMPLETED</button>
            </div>
        </div>

    </div>
    <div class="empty-box"></div>
</div>



<style>
    .button-topics{
        width: 97%;
        text-align: left;
        padding-left: 20px;
        margin: 2px;
        border-radius: 5px;
    }
    .page{
        display: flex;
    }
    .topics{
        flex: 1 1 auto;
        border: 1px solid #888;
        max-width: 380px;
        margin: 10px auto;
        padding: 15px;
        border-radius: 10px;
        margin-right:10px;
    }
    .empty-box{
        flex: 1 1 auto;
    }
    .container {
        max-width: 600px;
        flex: 3 1  auto;
        border: 1px solid #888;
        margin: 10px auto;
        padding: 15px;
        border-radius: 10px;
    }
    .filter-btn{
        width: 70px;
        font-family: 'Oswald', sans-serif;
        cursor: pointer;
        border-radius: 8px;
    }
    .clear-btn{
         width: 70px;
         font-family: 'Oswald', sans-serif;
         cursor: pointer;
         border-radius: 8px;
     }
     .clear-btn:hover{
        background: rgb(234, 79, 36);
        color: white;
     }
    .title{
        font-family: 'Fjalla One', sans-serif;
            text-align: center;
            font-size: 39px;
            font-style: italic;

    }
    .active-topics{
        font-family: 'Oswald', sans-serif;
        margin-top:-10px;
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
       background: #d0d0d0;
       color:black;
    }
    button:focus {
        outline: none;
    }
    .active {
        background: rgb(67,81,175);
        color:white;
    }
</style>
