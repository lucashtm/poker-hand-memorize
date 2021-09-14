<script>
    import Card from './Card.svelte'

    const possibleRanks = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 12, 13];
    let deck = {
        S: [...possibleRanks],
        H: [...possibleRanks],
        D: [...possibleRanks],
        C: [...possibleRanks]
    };
    const suitChoices = ['C', 'D', 'H', 'S'];
    const boardSize = 5;
    const handSize = 2;
    const boardCards = [];
    const handCards = [];

    for (let i = 0; i < handSize; i++) {
        const suit = suitChoices[Math.floor(Math.random()*suitChoices.length)];
        const rank = deck[suit].splice(Math.floor(Math.random()*deck[suit].length), 1)[0];
        handCards.push({rank, suit});
    }

    for (let i = 0; i < boardSize; i++) {
        const suit = suitChoices[Math.floor(Math.random()*suitChoices.length)];
        const rank = deck[suit].splice(Math.floor(Math.random()*deck[suit].length), 1)[0];
        boardCards.push({rank, suit});
    }

</script>

<main>
    <div class="board card-list">
        {#each boardCards as card (card.suit + card.rank.toString(16))}
            <Card rank={card.rank+1} suit={card.suit} hidden={true} />
        {/each}
    </div>

    <div class="hand card-list">
        {#each handCards as card (card.suit + card.rank.toString(16))}
            <Card rank={card.rank+1} suit={card.suit} />
        {/each}
    </div>
</main>

<style>
    .card-list {
        display: flex;
    }
</style>
