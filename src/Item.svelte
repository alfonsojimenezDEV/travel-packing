<script>
    import {blurOnKey} from './util'

    export let item; // parámetro que recibirá el componente y que se corresponde con el item a pintar.
                     // este item será un objeto con varias propiedades como name y packed
    let editing = false; 
    
</script>  



<li>
    <input type="checkbox" bind:checked={item.packed} />
    {#if editing}
        <input bind:value={item.name} on:blur={() => (editing = false)}  type="text" 
            on:blur={() => (editing = false)}
            on:keydown={blurOnKey} />
    {:else}
        <span class="packed-{item.packed} on:click={() => (editing = true)}">{item.name}</span>
    {/if}
    <button class="icon">&#x1F5D1</button>
</li>

<style>
    /* Código de la página 72 */
    button {
        background-color: transparent;
        border: none;
    }

    input[type='checkbox'] {
        --size: 24px;
        height: var(--size);
        width: var(--size);
    }

    input[type='text'] {
        border: 1px solid lightgray;
    }

    li {
        display: flex;
        align-items: center;
    }
    
    .packed-true {
        color: gray;
        text-decoration: line-through;
    }

    span {
        margin: 0 10px;
    }
</style>