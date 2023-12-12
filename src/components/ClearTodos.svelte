<script lang="ts">
    export let clearCompleted
    export let completedTodos
</script>

<button
    on:click={clearCompleted}
    class:hidden={completedTodos === 0}
    class="clear-completed"
>
    Clear completed
</button>
