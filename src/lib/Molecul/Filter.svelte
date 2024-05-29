<script>
    import { createEventDispatcher } from 'svelte';
    import { SvgFilter } from '$lib';
    import { writable } from 'svelte/store';

    // Use a Svelte store for filters
    const filters = writable({ label: '' });

    const dispatch = createEventDispatcher();

    // Watch for changes in the filters store
    $: filters.subscribe(value => {
        dispatch('applyFilter', value);
    });
</script>

<form class="filter-controls" aria-label="Filter Controls">
    <label for="filter-select" class="sr-only">Select a filter</label>
    <div class="filter-select-wrapper">
        <SvgFilter class="filter-icon" aria-hidden="true"/>
        <select id="filter-select" bind:value={$filters.label} class="filter-select">
            <option value="">
                Filter
            </option>
            <option value="Zero Hungry">Zero Hungry</option>
            <option value="Clean Water and Sanitation">Clean Water and Sanitation</option>
            <option value="Quality Education">Quality Education</option>
            <option value="Good Health and well being">Good Health and well being</option>
            <!-- Add more options as needed -->
        </select>
    </div>
</form>

<style>
    .filter-controls {
        display: flex;
        align-items: center;
        gap: 16px;
        margin: 20px 40px;
        font-size: 1rem;
        font-weight: 600;
        color: var(--black);
    }

    /* Hide elements for screen readers only */
    .sr-only {
        position: absolute;
        width: 1px;
        height: 1px;
        padding: 0;
        margin: -1px;
        overflow: hidden;
        clip: rect(0, 0, 0, 0);
        border: 0;
    }

    /* Wrapper for select and icon */
    .filter-select-wrapper {
        position: relative;
        display: flex;
        align-items: center;
    }

    /* Styles for the select dropdown */
    .filter-select {
        padding: 8px 16px;
        font-size: 1rem;
        border-radius: 4px;
        border: 1px solid #ccc;
        background-color: var(--light-gray);
        font-family: var(--font-family-sans-serif);
        font-weight: 600;
        transition: background-color 0.2s, border-color 0.2s;
        appearance: none;
        background-image: url('data:image/svg+xml;base64,<svg xmlns="http://www.w3.org/2000/svg" width="10" height="10" viewBox="0 0 24 24"><path fill="none" stroke="currentColor" stroke-width="2" d="M7 10l5 5 5-5"/></svg>');
        background-repeat: no-repeat;
        background-position: right 12px center;
        background-size: 10px 10px;
    }

    .filter-select:focus {
        border-color: var(--primary-color);
        background-color: var(--white);
    }

    .filter-select-wrapper::before {
        content: '';
        position: absolute;
        right: 16px;
        width: 10px;
        height: 10px;
        pointer-events: none;
    }

    /* SvgFilter icon styles */
    .filter-icon {
        margin-right: 8px;
    }

    .filter-select-wrapper:hover .filter-icon path {
        fill: var(--primary-color);
    }
</style>
