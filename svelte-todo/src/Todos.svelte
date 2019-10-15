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
</script>