<script>
    import {blurOnKey} from './util'

    export let item; // parámetro que recibirá el componente y que se corresponde con el item a pintar.
                     // este item será un objeto con varias propiedades como name y packed
    let editing = false; 
    
</script>  

<h2>Prueba de item</h2>

<li>
    <input type="checkbox" bind:value={item.packed} />
    {#if editing}
        <input bind:value={item.name} on:blur={() => (editing = false)}  type="text" />
    {:else}
        <span class="packed-{item.packed} on:click={() => (editing = true)}">{item.name}</span>
    {/if}
    <button class="icon">&#x1F5D1</button>
</li>

<style>
    /* falta añadir el style de la página 72 */
</style>