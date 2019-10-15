<div class="todo-item">
    <div class="todo-item-left" transition:fly="{{ y: 20, duration: 300 }}">
        <input type="checkbox" bind:checked={completed} on:change={toggleComplete}>
        <div class="todo-item-label" class:completed={completed}>{title}</div>
    </div>
    <div class="remove-item" on:click={deleteTodo}>
        ×
    </div>
</div>