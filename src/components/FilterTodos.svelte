<script>
    export let selectedFilter;
    export let setFilter;

    let filters = ['all', 'active', 'completed'];
</script>

<div class="filters">
    {#each filters as filter}
        <button
            on:click={() => setFilter(filter)}
            class:selected={selectedFilter === filter}
            class="filter"
        >
        {filter}
        </button>
    {/each}
</div>

<style>
  .filters {
    display: flex;
    gap: var(--spacing-4);
  }

  .filter {
    text-transform: capitalize;
    padding: var(--spacing-4) var(--spacing-8);
    border: 1px solid transparent;
    border-radius: var(--radius-base);
  }

  .filter:hover {
    border: 1px solid var(--color-highlight);
  }

  .selected {
    border-color: var(--color-highlight);
  }
</style>