<script>
  let active = true;
  let todos = [];
  let todoField = "";
</script>

{todos}

{#if todos.length === 0}
  <p class="empty-message">Pas de tâches pour le moment !</p>
{/if}

{#each todos as todo, i}
  <p>
    <input type="checkbox" name="done" id="done" bind:checked={todo.done} />
    <span>{i + 1}: {todo.text}</span>
    <button
      on:click|preventDefault={() => {
        todos = todos.filter((t) => t !== todo);
      }}>X</button
    >
  </p>
{/each}

<form
  on:submit|preventDefault={() => {
    if (todoField === "") {
      alert("Merci de rentrer une tâche");
    } else {
      todos = [
        ...todos,
        { number: todos.length + 1, text: todoField, done: false },
      ];
      todoField = "";
    }
  }}
>
  <input
    type="text"
    name="todo"
    id="todo"
    bind:value={todoField}
    placeholder="Acheter des fraises..."
  />
  <button>+</button>
</form>
<button
  on:click|preventDefault={() => {
    todos = [];
  }}>Tout supprimer</button
>

<style>
  :global(body) {
    font-family: "Arial", sans-serif;
    background-color: #f0f4f8;
    margin: 0;
    padding: 20px;
  }

  form {
    display: flex;
    justify-content: space-between;
    margin-bottom: 20px;
  }

  input[type="text"] {
    flex-grow: 1;
    padding: 10px;
    font-size: 16px;
    border: 1px solid #ccc;
    border-radius: 4px;
    margin-right: 10px;
  }

  button {
    background-color: #007bff;
    color: white;
    border: none;
    padding: 10px 20px;
    font-size: 16px;
    cursor: pointer;
    border-radius: 4px;
    transition: background-color 0.3s ease;
  }

  button:hover {
    background-color: #0056b3;
  }

  p {
    display: flex;
    align-items: center;
    background-color: white;
    padding: 10px;
    border-radius: 5px;
    margin-bottom: 10px;
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
  }

  input[type="checkbox"] {
    margin-right: 10px;
  }

  p button {
    margin-left: auto;
    background-color: #dc3545;
  }

  p button:hover {
    background-color: #c82333;
  }

  p button:focus {
    outline: none;
  }

  p span {
    flex-grow: 1;
  }

  .empty-message {
    font-size: 18px;
    color: #666;
    text-align: center;
    margin: 20px 0;
  }
</style>
