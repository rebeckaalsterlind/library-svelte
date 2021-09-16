<script>

	import { afterUpdate, beforeUpdate, onMount } from 'svelte';
	import Books from './Books.svelte';
	import Form from './Form.svelte'
	export let books = [];

	const getBooks = () => {

		fetch("http://localhost:3000/books")
		.then(res => res.json())
		.then(data => {
			books = data
		})

	}

  onMount(() => getBooks())
	

	const addBook = (newBook) => {
	//	const newBook = evt.detail;

		fetch(`http://localhost:3000/books`, {
			method: "post",
			headers: {
				"Content-Type": "application/json",
			},
   	 	body: JSON.stringify(newBook)
		})
	
		getBooks();

	}

</script>



<main>
  <h2>My library!</h2>
 <Books {books}/>
 <Form {addBook} />
</main>



<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}
</style>