<script>
	import Recipe from './components/Recipe.svelte'
	let query 
	let recipes = []
	let visNummer = true
	let y = 0
	
	$: fetch('https://www.themealdb.com/api/json/v1/1/search.php?s=' + query)
	.then(res => res.json())
	.then(json=>{
		console.log(json)
		if(json.meals) recipes = json.meals
	})
	
</script>

<header>

	<button on:click={() => visNummer = !visNummer}> {visNummer ? 'Hide Numbers' : 'Show Numbers'}  </button>
	<div class="query">
		<input bind:value={query} type="text">
	</div>
</header>
<main>
	{#each recipes as recipe, index}
		<Recipe 	 {visNummer} {recipe} index = {index}/>
	{/each}
</main>

<style>
	main{
		display:grid;
		grid-template-columns: repeat(auto-fill, minmax(400px, 1fr));
		place-items:center;
		gap:1rem;
		position: relative;

	}
	header{
		display:grid;
		grid-template-columns: 1fr;
		place-items:center;
		padding:1rem;
		background-color: cornflowerblue;
		margin-bottom:.5rem;
	}
	button{
		position: absolute;
		left: 1rem;
		z-index: 1;
		color: white;
		background-color: grey;
		border: 1px solid black;
		border-radius: .5rem ;
		/* height: 2rem; */

	}
		button:hover{
			background-image: linear-gradient(90deg, #00C0FF 0%, #FFCF00 49%, #FC4F4F 80%, #00C0FF 100%);
   			animation:slidebg 5s linear infinite;

	}
	@keyframes slidebg {
  to {
    background-position:20vw;
  }
}

</style>