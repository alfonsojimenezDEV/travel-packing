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
        //alert ('Add Item');
        //Código página 74
        //Código para comprobar si el nombre del item está duplicado

        const duplicate = Object.values(categories).some(cat => Object.values(cat.items).some(item => item.name===itemName) );
        if (duplicate) {
            message = `This item "${itemName}" already exists.`;
            alert(message);
            return; 
        }

        const {items} = category;
        const id = getGuid();
        
        items[id] = {id, name: itemName, packed:false}; // Se crea el elemento
        category.items = items; 
        itemName = '';
    }


</script>


<section>
    
    <h3>
        {#if editing}
            <input  bind:value={category.name} 
                    on:blur={() => (editing = false)}
                    on:keypress={blurOnKey}>
        {:else}
             <span on:click={() => (editing=true)}>{category.name}</span>
        {/if}
        <span class="status">{status}</span>
        <button class="icon">&#x1F5D1</button>
    </h3>

    <!-- Código página 75 -->
    <form action="" on:submit|preventDefault={addItem}>
        <label for="">
            New Item
            <input type="text" bind:value={itemName}>
        </label>
        <button disabled={!itemName}>Add Item</button>
    </form>

    <ul>
        {#each itemsToShow as item(item.id)}
            <Item bind:item/>
        {:else}
             <div>This category does not contain any items yet.</div>
        {/each}
    </ul>
</section>

<style>
    /* Código del style de página 75 */
    button, input {
        border: solid lightgray 1px;
    }

    button.icon {
        border: none;
        background-color: transparent;
    }

    h3 {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin: 0;
    }

    section {
        --padding: 10px;

        background-color: white;
        border: solid transparent 3px;
        border-radius: var(--padding);
        color: black;
        display: inline-block;
        margin: var(--padding);
        padding: calc(var(--padding) * 2);
        padding-top: var(--padding);
        vertical-align: top;
        min-width: 400px;
    }

    .status {
        font-size: 18px;
        font-weight: normal;
        margin: 0 15px;
    }

    ul {
        list-style: none;
        margin: 0;
        padding-left: 0;
    }

</style>