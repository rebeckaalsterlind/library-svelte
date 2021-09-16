<script>
  import { afterUpdate, beforeUpdate, onMount, createEventDispatcher } from 'svelte';
  export let addBook; 
  const dispatch = createEventDispatcher; 

  let newTitle;
  let newAuthor; 

  const handleSubmit = (evt) => {
    evt.preventDefault();   
    let randomNo = Math.floor(Math.random() * 900);
    addBook({id: randomNo, title: newTitle, author: newAuthor, rented: false});
  }

</script> 

<style>
</style>

<div>
  <form on:submit={handleSubmit}>
    <input id="title" type="text" placeholder="Title.. " bind:value={newTitle}/>
    <input id="author" type="text" placeholder="Author.. " bind:value={newAuthor}/>
    <button>Save</button>
  </form>
</div>
