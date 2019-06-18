<template>
    <div class="card-container">
        <div class="game-card">
            <span class="title"> {{SetCardTitle}} </span>
            <span> {{SetCardText}} </span>
        </div>
        <div v-show="SetTimer" class = "timer">
            <b-progress :max="timerMax">
                <b-progress-bar :value="timerValue">
                    <div class="time">{{GetTime}}</div>
                </b-progress-bar>
            </b-progress>
            <b-button @click="StartTimer">Старт</b-button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'GamePanel',
    props: {
        card: Object,
        players: Array,
    },
    data: function () {
        return {
            cardText: "",
            codes: ['name', 'panish'],
            currentPlayers: [],
            timerMax: 0,
            timerValue: 0,
            timer: null,
            timerDate: null
        }
        
    },
    computed: {
        SetCardText: function () {
            //console.log("SetCardText")
            var str = this.card.text;
            str = str.split(/\{{(.*?)\}}/);

            var codes = this.codes; //Костыль. Я хз почему но без этой строчки codes is not defined     
            this.currentPlayers = this.players.slice();
            //console.log(this.players)
            
            for (var i = 0; i < str.length; i++)
            {
                if (this.codes.indexOf(str[i]) != -1 )
                {
                    str[i] = this.ReplaceCode(str[i]);
                }
            }

            str = str.join('');

            console.log(this.card.type);

            
            return str;            
        },
        SetCardTitle: function () {
            switch (this.card.type)
            {                
                case "virus":
                   return "вирус"
                case "virus-end":
                    return "вирус"
                case "simple":
                    return "";
                case "copy-shot":
                    return "внезапный шот"
            }

        },
        SetTimer: function () {
            if (this.card.timer !== undefined)
            {
                this.timerMax = this.card.timer*60;
                this.timerValue = this.card.timer*60;
                return true;
            }
            else
            {
                return false;
            }
        }, 
        GetTime: function () {
            var result = "";
            var min = Math.ceil(this.timerValue/60);
            var sec = this.timerValue % 60;

            if (sec < 10)
            {
                sec = '0' + sec;
            }

            result = min + ":" + sec;
            
            return result;
        }
    },
    methods:
    {
        ReplaceCode: function(code) {
            var index;
            var result;
            //console.log("code");
            switch(code)
            {                
                case "name":
                    //console.log("switch - name");                    
                    index = this.RngInt(1, this.currentPlayers.length - 1);                    
                    result = this.currentPlayers[index];                    
                    this.currentPlayers.splice(index,index);
                    //console.log(this.currentPlayers)
                    return result;
                case "panish":
                    switch (this.card.mode)
                    {
                        case 1:
                            return this.RngInt(1, 3) + " глотка(ов)";
                        case 2:
                            return this.RngInt(4, 6);
                        case 3:
                            var value = this.RngInt(1, 3);

                            if (value == 1)
                            {
                                return 7
                            }
                            if (value == 2)
                            {
                                return "до дна"
                            }
                            if (value == 3)
                            {
                                return "шот"
                            }
                    }
            }
        },
        RngInt: function(min, max) {
            return min + Math.floor(Math.random() * (max - min + 1));
        },
        StartTimer: function () {
            var self = this;
            this.timer = setInterval(function() {
                this.timerValue--;
                console.log(this.timerValue)
            }.bind(this), 1000)
        },
        /*SetCardText: function () {
            var str = this.card.text;    
            var codes = this.codes; //Костыль. Я хз почему но без этой строчки codes is not defined        
            //console.log(this.codes)

            for (var i = 0; i < this.codes.length; i++)
            {
                console.log("kyky")
                str.replace(new RegExp(codes[i], 'g'), this.ReplaceCode(codes[i]))
            }   
        }*/
    },
    watch: {
        card: function () {
            //console.log("watch card")
            //this.currentPlayers = this.players;
            //this.SetCardText();
        },
        /*players: function () {
            console.log("watch players")
            this.currentPlayers = this.players;
            this.SetCardText();
        }*/
    },  
    beforeUpdate: function () {
        //console.log("bU");
    }  
    
}
</script>

<style>
    .game-card
    {
        background-color: white;
        margin: 15px;
        padding: 15px;
        border-radius: 10px;

        font-size: 18px;
        font-weight: 500;

        box-shadow: 5px 5px 10px rgba(0,0,0,0.4)!important;
    }
    .game-card .title
    {
        display: block;
        text-transform: uppercase;
        font-size: 20px;
        font-weight: 600;
    }
    .timer
    {
        background-color: white;
        margin: 15px;
        padding: 15px;
        border-radius: 10px;
    }
    .progress
    {
        position: relative;
        margin-bottom: 15px;
        height: 1.5rem;
    }
    .time
    {
        position: absolute;
        left:50%;
        transform: translateX(-50%);
        font-size: 15px;
    }
</style>
