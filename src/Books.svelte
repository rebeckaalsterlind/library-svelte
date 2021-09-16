<script>
  import { afterUpdate, beforeUpdate, onMount } from 'svelte';
  import Book from './Book.svelte'
  export let books;
</script> 

<div>
  {#each books as book}
    <Book {book} />
  {:else}
    <p>Fetching books...</p> 
  {/each}
</div>



<style>
</style>
