<script>
    import Category from './Category.svelte';
    import {getGuid, sortOnName} from './util.js'

    let categoryArray = [];
    let categories = {};
    let categoryName;
    let message = '';
    let show = 'all';

    $: categoryArray = sortOnName(Object.values(categories));

    function addCategory() {
        // Falta código página 77
        // alert('Se ha pulsado el botón de Añadir una categoría')
        // Falta el código que comprueba si la categoría está duplicada.

        const id = getGuid();
        categories[id] = {id, name: categoryName, items: {}};
        categories = categories // Esto provoca un update y, por tanto una reacción.
        categoryName = '';
        
    }

    function clearAllChecks() {
        // Falta código página 77
    }


</script>

<section>
    <!-- <p>Prueba de Checklist</p> -->
    <header>
        <form action="" on:submit|preventDefault={addCategory}>
            <label for="">
                New Category
                <input type="text" bind:value={categoryName}>
            </label>
            <button disabled={!categoryName}>Add Category</button>
            <button class="logout-btn">Log Out</button>
        </form>
        <p>
            Suggested categories include Backpack, Clothes, 
            <br>
            Last Minute, Medicines, Running Gear, and Toiletries.
        </p>

        <div class="radios">
            <label for="">Show</label>
            <label for="">
                <input type="radio" name="show" value="all" bind:group={show}>
                All
            </label>

            <label for="">
                <input type="radio" name="show" value="packed" bind:group={show}>
                All
            </label>

            <label for="">
                <input type="radio" name="show" value="unpacked" bind:group={show}>
                All
            </label>
            <button class="clear" on:click={clearAllChecks}>Clear All Checks</button>
        </div>
    </header>

    <div class="categories">
        {#each categoryArray as category(category.id)}
            <Category bind:category {categories} {show} />
            
        {/each}
    </div>
</section>

<style>
    /* Código página 78 */
    .categories {
        display: inline-flex;

    }
</style>