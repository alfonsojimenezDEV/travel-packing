<script>
    import Item from './Item.svelte';
    import {getGuid, blurOnKey, sortOnName} from './util';

    export let categories; // Is used to determine whether an item to be added already exists in another category
    export let category;   // It describes the category being rendered 
    export let show;       // it is a string with a value of all, packed, or unpacked. It indicates which of the items should be displayed

    let editing = false;
    let itemName = '';
    let items = [];
    let message = '';
    
    $: items = Object.values(category.items); // se convierte en un array los objetos que son los items de la categoría que se pasa como parámentro
    $: remaining = items.filter(item => !item.packed).length; // captura los items que faltan. Cuenta los items que hay en el array que devuelve la función filter
    $: total = items.length; // total de items que tiene la categoría
    $: status = `${remaining} of ${total} remaining`;
    $: itemsToShow = sortOnName(items.filter(i => shouldShow(show, i)));

    function shouldShow(show, item) {
        return (
            show === 'all' || (show ==='packed' && item.packed) || (show === 'unpacked' && !item.packed)
        );
    }

    function addItem() {
        alert ('Add Item');
        //Falta código página 74
    }

</script>


<section>
    <h2>Prueba desde Category</h2>
    
    <h3>
        {#if editing}
            <input  bind:value={category.name} 
                    on:blur={() => (editing = false)}
                    on:keypress={blurOnKey}>
        {:else}
             <span on:click={() => (editing=true)}>{category.name}</span>
        {/if}
    </h3>

    <!-- //Falta codigo form on:submit página 75 -->

    <ul>
        {#each itemsToShow as item(item.id)}
            <Item bind:item/>
        {:else}
             <div>This category does not contain any items yet.</div>
        {/each}
    </ul>
</section>

<style>
    /* Falta el código del style de página 75 */
</style>