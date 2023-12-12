<script>
    export let incompleteTodos;
</script>

<span class="todo-count">
    {incompleteTodos}
    {incompleteTodos === 1 ? 'task' : 'tasks'} left
</span>