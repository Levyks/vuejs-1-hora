<script>
  import FormTodo from './FormTodo.svelte';

  let comments = [];
  let commentsFormated = [];

  function addComment(event) {
    comments.push(event.detail);
    comments = comments;
  }

  function removeComment(index) {
    comments.splice(index, 1);
    comments = comments;
  }

  $: commentsFormated = comments.map(comment => ({
    ...comment,
    name: comment.name && comment.name.trim() ? comment.name : 'Anônimo'
  }));

</script>

<div class="container">
  <h1>Comentários</h1>
  <hr />
  <FormTodo on:add-todo={addComment} />
  <div class="list-group">
    {#if commentsFormated.length}
      {#each commentsFormated as comment, index}
        <div class="list-group-item">
            <span class="comment__author">Autor: <strong>{ comment.name.trim() || 'Anônimo' }</strong></span>
            <p>{ comment.message }</p>
            <div>
              <a href={'#'} title="Excluir" on:click|preventDefault={() => removeComment(index)}>Excluir</a>
            </div>
        </div>
      {/each}
    {:else}
      <p>Sem comentários...</p>
    {/if}
  </div>
  <hr />
</div>