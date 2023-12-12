<script>
    export let incompletedTodos;
</script>

<span class="todo-count">
    {incompletedTodos}
    {incompletedTodos === 1 ? 'task' : 'tasks'} left
</span>