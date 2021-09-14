<script>
    import Card from './Card.svelte';
    export let suit;
    const totalCards = 14;
    const cardToSkip = 11;

</script>

<main>
    {#each Array(totalCards) as _, index (index)}
        {#if index != cardToSkip}
            <Card suit={suit} rank={index+1} />
        {/if}
    {/each}
</main>

<style>
    main {
        display: flex;
        justify-content: space-around;
    }
</style>
