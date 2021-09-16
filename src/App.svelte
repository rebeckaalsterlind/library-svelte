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



<div>
		<header>
			<h1>My Svelte<br />library</h1>
			<Form {addBook} />
		</header>
		<Books {books}/>
</div>



<style>
	div {
		text-align: center;
		padding: 2em;
		display: flex;
		flex-flow: row wrap;
	}

	header {
		margin-top: 50px;
		width: 100%;
		display: flex;
		flex-flow: row nowrap;
		justify-content: space-evenly;
	}

	h1 {
		color: rgb(22, 3, 30);
		text-shadow: .5px .5px 3px gold;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 900;
	}
</style>