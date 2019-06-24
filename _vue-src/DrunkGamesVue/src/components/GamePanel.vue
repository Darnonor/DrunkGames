<template>
    <div class = "game-panel">
        <b-progress :value="currentCard+1" :max="cards.length" show-value ></b-progress>
        <Card :card="cards[currentCard]" :players="players" ></Card>
        <b-button @click="SwitchCard" class="shadow" variant="light">Продолжить</b-button>
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
        margin-bottom: 25px;   
        
        border-radius: 0;
    }
    .game-panel .progress
    {
        width: 100%;
        border-radius: 0;
        height: 15px;
    }
    .game-panel .progress-bar
    {
        background-color: #f12711;  
    }
    .game-panel
    {
        height: 100%;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: space-between;
        
    }
</style>
