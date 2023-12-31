<script>
    import { fade, slide } from 'svelte/transition';

    export let todo;
    export let completeTodo;
    export let removeTodo;
    export let editTodo;
    export let duration;

    let editing = false;

    function toggleEdit() {
        editing = true;
    }

    function handleEdit(e, id) {
        let pressedKey = e.key;
        let targetElement = e.target instanceof HTMLInputElement;
        let newTodo = e.target.value;
        switch(pressedKey) {
            case 'Escape':
                if (targetElement) {
                    e.target.blur();
                }
                break;
            case 'Enter':
                if (targetElement) {
                    editTodo(id, newTodo);
                    e.target.blur();
                }
                break;
        }
    }

    function handleBlur(e, id) {
        if (e.target instanceof HTMLInputElement) {
            let newTodo = e.target.value;
            editTodo(id, newTodo);
            e.target.blur();
            editing = false;
        }
    }
</script>

<li 
    in:slide={{ duration }}
    out:fade={{ duration }}
    class:editing 
    class="todo"
>
    <div class="todo-item">
        <div>
            <input
                on:change={() => completeTodo(todo.id)}
                checked={todo.completed}
                id="todo" 
                class="toggle" 
                type="checkbox" 
            />
            <label 
                aria-label="Check todo" 
                class="todo-check" 
                for="todo" 
            />
        </div>
        <span 
            on:dblclick={toggleEdit}
            class:completed={todo.completed} 
            class="todo-text"
        >{todo.text}</span>
        <button 
            on:click={() => removeTodo(todo.id)}
            aria-label="Remove todo" 
            class="remove" 
        />
    </div>
    {#if editing}
        <input 
            on:keydown={(e) => handleEdit(e, todo.id)}
            on:blur={(e) => handleBlur(e, todo.id)}
            class="edit" 
            type="text" 
            value={todo.text}
            autofocus 
        />
    {/if}
</li>

<style>
  .todo {
    font-size: var(--font-24);
    font-weight: 400;
    border-bottom: 1px solid #ededed;
  }

  .todo:last-child {
    border-bottom: none;
  }

  .todo-check,
  .todo-text {
    display: block;
    padding: var(--spacing-16);
    color: var(--color-gray-28);
    transition: color 0.4s;
  }

  .todo-check {
    border-radius: 100%;
  }

  .completed {
    color: var(--color-gray-58);
    text-decoration: line-through;
  }

  .todo-item {
    position: relative;
    display: flex;
    align-items: center;
    padding: 0 var(--spacing-8);
  }

  .editing .todo-item {
    display: none;
  }

  .edit {
    width: 100%;
    padding: var(--spacing-8);
    font-size: var(--font-24);
    border: 1px solid #999;
    border-radius: var(--radius-base);
    box-shadow: inset 0 -1px 5px 0 var(--shadow-1);
  }

  .toggle {
    position: absolute;
    top: 26px;
    left: 13px;
    transform: scale(2);
    opacity: 0;
  }

  .toggle + label {
    background-image: url('data:image/svg+xml;utf8,%3Csvg%20xmlns%3D%22http%3A//www.w3.org/2000/svg%22%20width%3D%2240%22%20height%3D%2240%22%20viewBox%3D%22-10%20-18%20100%20135%22%3E%3Ccircle%20cx%3D%2250%22%20cy%3D%2250%22%20r%3D%2250%22%20fill%3D%22none%22%20stroke%3D%22%23949494%22%20stroke-width%3D%223%22/%3E%3C/svg%3E');
    background-repeat: no-repeat;
    background-position: 84% 50%;
  }

  .toggle:checked + label {
    background-image: url('data:image/svg+xml;utf8,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20width%3D%2240%22%20height%3D%2240%22%20viewBox%3D%22-10%20-18%20100%20135%22%3E%3Ccircle%20cx%3D%2250%22%20cy%3D%2250%22%20r%3D%2250%22%20fill%3D%22none%22%20stroke%3D%22%2359A193%22%20stroke-width%3D%223%22%2F%3E%3Cpath%20fill%3D%22%233EA390%22%20d%3D%22M72%2025L42%2071%2027%2056l-4%204%2020%2020%2034-52z%22%2F%3E%3C%2Fsvg%3E');
  }

  .remove {
    display: none;
    margin-left: auto;
    font-size: var(--font-32);
    color: var(--color-gray-58);
    transition: color 0.2s ease-out;
  }

  .remove:hover {
    color: var(--color-highlight);
  }

  .remove:after {
    content: '×';
  }

  .todo:hover .remove {
    display: block;
  }
</style>