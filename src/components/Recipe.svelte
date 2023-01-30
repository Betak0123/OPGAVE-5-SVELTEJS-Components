<script>
    export let recipe // javascript objekt med en hel opskrift
    export let index
    import Page from "./Page.svelte";
	import {blur} from 'svelte/transition'
	import {fade} from 'svelte/transition'
	import {fly} from 'svelte/transition'
    export let visNummer
    let y

    console.log(recipe)
    let active = false
	let ingridients = []
        // $: console.log(active)
    const ingridienser = () =>{
        ingridients = []
        y=0
        for (let i = 0; i < 20; i++) {
            let text1 = 'strIngredient' + i
            let text2 = 'strMeasure' + i
            if(!recipe[text1] == '' || !recipe[text1] == null){
                ingridients = [...ingridients , {ting: recipe[text1], mængde: recipe[text2]}]
            }

            // console.log(recipe[text])
        }
        console.log(ingridients)
    }
</script>

<svelte:window bind:scrollY={y}/>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<main in:fly="{{ y: 200, duration: 1500 }}" out:blur on:click={() => {
    active = !active 
    ingridienser()

}} class={active ? 'active' : ''} style='background-image:url({recipe.strMealThumb});'>

    {#if visNummer}
        <Page number = {index}/>
    {/if}

    <h1>{recipe.strMeal}</h1>
    {#if active}
    <div id="instructions" in:blur>
        
        <p>Instructions: <br>{recipe.strInstructions}</p>
    </div>
    <div id="ingridients" in:blur>
        <p>Ingridients:</p>
        <div class="samling">
            {#each ingridients as food}
            <p class="ingridiens">{food.ting}: {food.mængde}</p>
            {/each}
        </div>
    </div>
    {/if}

</main>

<style>
    main{
        height:400px;
        width:100%;
        display:grid;
        place-items:center;
        font-weight: 100;
        color:white;
        border-radius:1rem;
        border: 2px solid black;
        position: relative;

    }
    h1{
        background-color: rgba(255, 255, 255, 0.742);
        color: black;
        border-radius: 1rem;
        padding: .5rem;
        font-size: larger;
    }
    .active{
        transition: all 1s ease-in-out;
        width: 98vw;
        height: 100vh;
        position: absolute;
        top: 0;
        left: 0;
        background-size: cover;
        display: grid;
        grid-template-rows: 1fr 1fr 1fr;
        padding: 1rem;
        z-index: 2;
    }
    
    p{
        background-color: rgba(255, 255, 255, 0.742);
        color: black;
        border-radius: 1rem;
        padding: .5rem;
        font-weight: 400;
        width: fit-content;
        border: 1px solid black;
    }
    .samling{
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
        width: 89vw;
        gap: 1rem;
    }
    .ingridiens{
        width: 100px;
        display: grid;
        place-items: center;
        font-size: small;
    }


</style>