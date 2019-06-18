<template>
    <div class = "game-panel">
        <Card :card="cards[currentCard]" :players="players" ></Card>
        <b-button @click="SwitchCard" variant="light">Продолжить</b-button>
    </div>
</template>

<script>
import Card from './Card.vue'
export default {
    name: 'GamePanel',
    components: {
        Card,
    },
    props: {
        cards: Array,
        players: Array
    },
    data: function () {
        return {
            currentCard: 0,
        }
    },
    methods: 
    {
        SwitchCard: function() {
            if (this.currentCard + 1 < this.cards.length)
            {
                this.currentCard++;
            }
            else
            {
                this.$emit("EndGame");
            }
        }
    }
}
</script>

<style>
    .game-panel .btn
    {
        padding: 5px 25px;
        font-size: 16px;
         
    }
</style>
