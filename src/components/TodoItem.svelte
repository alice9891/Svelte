<script>
    export let todo;
    export let handleCheckTodo;
</script>

<input type="checkbox"
bind:checked={todo.done}
onclick={() => handleCheckTodo(todo.id)}>
<span>{todo.content}</span>
<a href="#!">X</a>