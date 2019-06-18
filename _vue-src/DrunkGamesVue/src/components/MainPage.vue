<template>
    <div class="container main-page">
        <div class="logo">
            <span>АлкоИгрища</span>
        </div>
        <PlayersPanel @AddNewPlayer="AddNewPlayer" :players="players" :defaultCountPlayers="defaultCountPlayers"></PlayersPanel>

        <b-button @click="StartGame" class="btn-play">
            <div class="font-icon">
                <font-awesome-icon icon="play" />
            </div> 
            Начать
        </b-button>
    </div>
</template>

<script>
import PlayersPanel from './PlayersPanel.vue'

export default {
    name: 'MainPage',
    components: {
        PlayersPanel
    },
    props: {
        //msg: String
        defaultCountPlayers: Number,
    },
    data: function () {
        return {
            players: [],
            //defaultCountPlayers: 2,
            currentCountPlayers: Number
        }
    },
    methods: 
    {
        StartGame: function () {
            this.$emit("SetPlayers", this.players, this.currentCountPlayers)
            //console.log(this.players);
        },
        AddNewPlayer: function (newValue) {
            this.currentCountPlayers = newValue
            //console.log(newValue)
        }
    },
    mounted: function () {
        this.currentCountPlayers = this.defaultCountPlayers;
    }
}
</script>

<style>
    .logo
    {
        font-family: 'Lobster', cursive;
        /*font-family: 'El Messiri', sans-serif;*/
        font-size: 52px;
        color: white;
        margin-top: 35px;
        margin-bottom: 35px;
    }

    .main-page
    {
        height: 100%;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: space-between;
        padding: 15px;
        
        text-align: center;
        height: 100%;
    }

    .main-page .btn-play
    {
        /*box-shadow: none!important;*/
        box-shadow: 5px 5px 10px rgba(0,0,0,0.4)!important;
        font-size: 24px;
        font-weight: 500;
        background-color: #f39c12;
        border: none;
        display: flex;
        
        /*padding-top: 10px;
        padding-bottom: 10px;*/
        padding: 10px 25px;
        align-items: center;
        margin-bottom: 45px;
        border-radius: 15px;
        
    }

    .font-icon
    {
        display: inline;
        font-size: 14px;
        margin-right: 10px;
    }
</style>
