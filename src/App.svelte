<script>
  let todos = [];
  let newTodoText = "";

  function addTodo() {
    newTodoText.trim();

    if (!newTodoText) {
      return;
    }

    const todo = { id: Date.now(), text: newTodoText, isComplete: false };

    todos = [...todos, todo];

    newTodoText = "";
  }

  function deleteTodo(id) {
    todos = todos.filter((todo) => todo.id !== id);
  }
</script>

<form on:submit|preventDefault={addTodo}>
  <input type="text" bind:value={newTodoText} />
  <button>Add</button>
</form>

<ul>
  {#each todos as todo (todo.id)}
    <li>
      <input bind:checked={todo.isComplete} type="checkbox" />
      <span class:todo-complete={todo.isComplete}>{todo.text}</span>
      <button on:click={() => deleteTodo(todo.id)}>Delete</button>
    </li>
  {/each}
</ul>

<style>
  .todo-complete {
    text-decoration: line-through;
  }
</style>
