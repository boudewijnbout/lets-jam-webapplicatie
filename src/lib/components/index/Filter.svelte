<script>
    import {enhance} from "$app/forms";
    import {onMount} from "svelte";

    // Components
    import RangeSlider from "../RangeSlider.svelte";
    import Checkbox from "../Checkbox.svelte";

    // Stores
    import {filterState} from "$lib/stores/showFilter.js";

    // Get data
    export let tags;
    export let title;
</script>

<!-- Filter wrapper -->
<div class="filter-wrapper" class:visible={$filterState === true}>

    <!-- Filter title -->
    <h5>{title}</h5>
    <p>Aantal reacties</p>

    <!-- Custom rangeslider -->
    <div class="rangeslider-wrapper">
        <p>0</p>
        <RangeSlider min="0" max="500" value="0"/>
        <p>1000</p>
    </div>

    <!-- Categories checkboxes -->
    <div class="categories-wrapper">
        <p>Categorieën</p>

        <form method="POST" action="?/checkboxFilter" use:enhance>
            {#each tags as tag}
                <Checkbox
                        name="checkbox"
                        value={tag.id}
                        emoji={tag.emoji_name}
                        label={tag.name}
                />
            {/each}

            <!-- Apply filter button -->
            <button type="submit">Apply filters</button>
        </form>
    </div>
</div>

<style>
    .filter-wrapper {
        background-color: var(--element-white);
        padding: 1.25rem 1.6rem;
        border-radius: 0.6rem;
        box-shadow: rgb(149 157 165 / 20%) 0px 8px 24px;
        position: fixed;
        right: 0;
        bottom: 1rem;
        transform: translateX(100%);
        transition: transform 200ms;
    }

    h5 {
        font-size: 1.25rem;
    }

    p {
        margin-top: 1.25rem;
        font-family: "Montserrat", sans-serif;
        margin-bottom: 0.6rem;
        font-size: 0.85rem;
    }

    .rangeslider-wrapper {
        display: flex;
        align-items: center;
    }

    .rangeslider-wrapper p {
        margin: 0;
        font-family: "Rubik", sans-serif;
        color: var(--element-primary);
        font-weight: 500;
    }

    .categories-wrapper {
        display: flex;
        flex-direction: column;
    }

    .visible {
        transform: translateX(0);
        right: 0.5rem;
    }

    button {
        background-color: var(--element-primary);
        padding: 0.5rem 0.5rem;
        border-radius: 5px;
        margin-top: 1rem;
        cursor: pointer;
        transition: background-color 150ms;
    }

    button:hover {
        background-color: var(--element-primary-action);
    }

    @media (min-width: 60rem) {
        .filter-wrapper {
            position: relative;
            transform: none;
            transition: none;
            margin-bottom: 1.5rem;
            bottom: 0;
        }
    }
</style>
