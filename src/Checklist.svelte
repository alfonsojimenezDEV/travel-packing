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
        // Código página 77
        // alert('Se ha pulsado el botón de Añadir una categoría')
        const duplicate = Object.values(categories).some(cat => cat.name === categoryName);
        
        if (duplicate) {
            message = `The category "${categoryName}" already exists.`;
            alert(message);
            return;
        }

        const id = getGuid();
        categories[id] = {id, name: categoryName, items: {}};
        categories = categories // Esto provoca un update y, por tanto una reacción.
        categoryName = '';
        
    }

    function clearAllChecks() {
        // Código página 77
        for (const category of Object.values(categories)) {
            for (const item of Object.values(category.items)) {
                item.packed = false;
            }
        }
        categories = categories;
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
                <input type="radio" name="show" value="all" bind:group={show}> <!-- Using bind:group with a set of related radio buttons makes the value a single string -->
                All
            </label>

            <label for="">
                <input type="radio" name="show" value="packed" bind:group={show}>
                Packed
            </label>

            <label for="">
                <input type="radio" name="show" value="unpacked" bind:group={show}>
                Unpacked
            </label>
            <button class="clear" on:click={clearAllChecks}>Clear All Checks</button>
        </div>
    </header>

    <div class="categories">
        {#each categoryArray as category(category.id)}
            <Category bind:category={category} bind:categories={categories} bind:show={show} />
            <!-- Esta línea se puede pone así, que es como viene en el libro -->
            <!-- <Category bind:category {categories} {show} /> -->
        {/each}
    </div>
</section>

<style>
    /* Código página 78 */
    .categories {
        display: inline-flex;
        flex-wrap: wrap;
        justify-content: center;
        
    }

    .clear {
        margin-left: 30px;
    }

    input[type='radio'] {
        --size: 12px;
        height: var(--size);
        width: var(--size);
        margin-left: 10px;
    }

    .logout-btn {
        position: absolute;
        right: 20px;
        top: 20px;
    }

    .radios {
        display: flex;
        align-items: center;
    }

    .radios > label:not(:first-of-type) {
        display: inline-flex;
        align-items: center;
    }
    .radios > label > input {
        margin-bottom: -3px;
        margin-right: 5px;
    }

    section {
        display: flex;
        flex-direction: column;
        align-items: center;
        font-size: 0.9em;
        margin-top: 1em;
    }

    
    

</style>