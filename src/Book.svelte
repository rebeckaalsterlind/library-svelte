<script>
  import { afterUpdate, beforeUpdate, onMount } from 'svelte';
  export let book = {};

  const handleClick = (evt) => {

  console.log('clicked',evt.target.id);




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
    .then(json => {
      console.log('json', json);
      book = json
    });






  }


</script> 

<style>
  article{
    border: 1px solid grey;
  }

  p{
    color: red;
  }
</style>

<article>
  <h3>Title: {book.title}</h3>
  <h5>Author: {book.author}</h5>
  {#if book.url !== undefined} 
  <img src={book.url} alt={book.title + " by " + book.author} height="100" />
  {/if}
  {#if book.rented}
  <p>rented</p>
  {:else}
  <button id={book.id} on:click={handleClick}>Rent book</button>
  {/if}
</article>
