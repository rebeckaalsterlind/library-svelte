<script>
  import { afterUpdate, beforeUpdate, onMount } from 'svelte';
  import Book from './Book.svelte'
  export let books;
</script> 

<main>
  {#each books as book}
    <Book {book} />
  {:else}
    <p>Fetching books...</p> 
  {/each}
</main>



<style>
  main {
    display: flex;
    flex-flow: row wrap;
    width: 100%;
    margin-top: 50px;
  }
</style>
