<script>
  import { afterUpdate, beforeUpdate, onMount } from 'svelte';
  export let book = {};

  const handleClick = (evt) => {

    fetch(`http://localhost:3000/books/${evt.target.id}`,  {
      method: "PATCH",
      headers: {
          "Content-Type" : "application/json"
        },
      body: JSON.stringify(
        {
          "rented": true
        }
      )
    })
    .then(response => response.json())
    .then(json => book = json);
  };

</script> 



<article>
  <header>
    <h3>{book.title}</h3>
    <h5>by:  {book.author}</h5>
  </header>
  <aside>
    {#if book.url !== undefined} 
      <img src={book.url} alt={book.title + " by " + book.author} height="100" />
    {/if}
  </aside>
  {#if book.rented}
  <button class="rented" disabled=true>Rented</button>
  {:else}
    <button class="available" id={book.id} on:click={handleClick}>Rent book</button>
  {/if}
</article>


<style>
  article{
    box-shadow: .1px .1px 10px rgb(33, 5, 44);
    display: flex;
    flex-flow: column wrap;
    align-items: center;
    margin: 0 1em 2em 1em;
    padding: 1em;
    min-width: 100px;
    background-color: rgba(255, 255, 255, 0.1);
  }

  h3 {
    margin: 0;
  }

  h5 {
    margin-top: 5px;
  }

  img {
    margin-bottom: 20px;
  }

  img:hover {
    transform: scale(2);
  }

  button {
    color: white;
    background-color: rgba(22, 3, 30, .50);
    border: 2px solid rgb(22, 3, 30);
    width: 100px;
  }

  .available:hover, .available:focus {
    box-shadow: .1px .1px 10px gold;
  }

  .rented {
    color: inherit;
    background-color:  rgba(22, 3, 30, .10);
    border: none;
  }
</style>