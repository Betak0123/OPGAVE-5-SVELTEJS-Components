
<script>
    export let number
    import {blur} from 'svelte/transition'
    // export let visNummer
</script>
<main in:blur out:blur>

    {number}
</main>
<style>
    main{
        position:absolute;
        right:1rem;
        bottom:1rem;
        width:2rem;
        height:2rem;
        background-color: rgba(255, 255, 255, 0.742);
        color:black;
        font-weight: 1000;
        display:grid;
        place-items:center;
        border-radius:50%;
    }
</style>