<template>
    <div class="players-panel">
        <b-form-input v-for="index in countPlayers" :key="index" v-model="players[index]" :placeholder="'Игрок ' + [[index]]"></b-form-input>
        
        <button v-on:click="AddNewPlayer" class="btn-plus"><font-awesome-icon icon="plus-circle" /></button>
    </div>
</template>

<script>
export default {
    name: 'PlayersPanel',
    props: {        
        players: Array,
        defaultCountPlayers: Number
    },
    data: function () {
        return {
            countPlayers: Number,           
        }
    },
    methods: {
        AddNewPlayer: function () {
            this.countPlayers++;
            this.$emit("AddNewPlayer", this.countPlayers)
        }
    },
    mounted: function () {
        this.countPlayers = this.defaultCountPlayers;
    }
}
</script>

<style>
    .players-panel
    {
        margin-bottom: 15px;
        text-align: left;
        display: inline-block;
        margin-bottom: 60px;
        overflow-x: auto;
    }
    .players-panel .form-control
    {
        margin-bottom: 15px;
        /*margin-left: auto;
        margin-right: auto;*/

        padding-left: 0;
        padding-right: 0;

        border-radius: 0;
        border: 0;
        border-bottom: 1px solid rgba(218, 243, 147, 0.7);

        background-color:initial;
        color:white;

        /*width:70%;*/

        font-size: 20px;    
    }

    .players-panel .form-control::-webkit-input-placeholder
    {
        color: rgba(255, 255, 255, 0.75);
    }

    .players-panel .form-control:focus
    {
        border: 0;
        border-bottom: 2px solid white;
        box-shadow: none;
    }

    .btn-plus 
    {
        background: none;
        border: none;
        color: white;
        font-size: 32px;
    } 
    .btn-plus:focus
    {
        outline: none!important;
    }   
</style>
