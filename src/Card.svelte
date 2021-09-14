<script>
    export let suit;
    export let rank;
    export let hidden = false;

    const unicodeTemplate = '&#x$;'
    const hiddenCard = '&#x1F0A0;'
    const cardBaseHex = 0x1f000;
    const suitMask = 0x000f0
    const rankMask = 0x0000f

    // Suits values
    const suitValues = {
        S: 0xa0, // Spades
        H: 0xb0, // Hearts
        D: 0xc0, // Diamonds
        C: 0xd0  // Clubs
    }

    let colorClass = 'black';

    function setColorClass() {
        colorClass = 'black';
        if(suit === 'H' || suit === 'D') {
            colorClass = 'red';
        }

        if (hidden) {
            colorClass = 'blue';
        }
    }

    function cardToUnicode() {
        if (hidden) {
            return hiddenCard;
        }
        const hexCode = cardBaseHex + suitValues[suit] + rank;
        return unicodeTemplate.replace('$', hexCode.toString(16));
    }

    function showCard() {
        hidden = false;
        setColorClass();
        cardUnicode = cardToUnicode();
    }

    setColorClass();
    $: cardUnicode = cardToUnicode();

</script>

<main>
    <span on:click={showCard} class="{colorClass}">{@html cardUnicode}</span>
</main>

<style>
    .blue {
        color: blue;
    }

    .red {
        color: red;
    }

    .black {
        color: black;
    }

    main {
        cursor: pointer;
        font-size: 10em;
    }
</style>
