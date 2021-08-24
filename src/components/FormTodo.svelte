<script>
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  let name;
  let message;

  function addComment() {
    if (message.trim() === '') {
      return;
    }
    dispatch('add-todo', {
      name, message
    });
    name = '';
    message = '';
  }
</script>


<div class="form-todo form-group">
  <p>
    <input placeholder="nome" type="text" name="author" class="form-control" bind:value={name}/>
  </p>
  <p>
    <textarea placeholder="Comentário" name="message"  class="form-control" bind:value={message}></textarea>
  </p>
  <button on:click={addComment} type="submit" class="btn btn-primary">Comentar</button>
</div>