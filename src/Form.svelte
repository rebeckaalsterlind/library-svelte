<script>
  import { afterUpdate, beforeUpdate, onMount, createEventDispatcher } from 'svelte';
  export let addBook; 
  const dispatch = createEventDispatcher; 

  let newTitle;
  let newAuthor; 

  const handleSubmit = (evt) => {
    evt.preventDefault();   
    let randomNo = Math.floor(Math.random() * 900);
    addBook({id: randomNo, title: newTitle, author: newAuthor, url: "img/noBook.png", rented: false});
  }

</script> 

<style>
  aside {    
    display: flex;
    flex-direction: column;
    align-items: center; 
    padding: 2em;
  }

  form {
    max-width: 200px;
  }

  h2 {
    font-size: 2em;
    margin: 0 0 5px 0;
  }

  button {
    color: white;
    background-color: rgba(22, 3, 30, .50);
    border: 2px solid rgb(22, 3, 30);
    width: 100px;
  }

  button:hover, button:focus {
    box-shadow: .1px .1px 10px gold;
  }

</style>
  
<aside>
  <h2>Add book:</h2>
  <form on:submit={handleSubmit}>
    <input id="title" type="text" placeholder="Title.. " bind:value={newTitle}/>
    <input id="author" type="text" placeholder="Author.. " bind:value={newAuthor}/>
    <button>Save</button>
  </form>

</aside>

