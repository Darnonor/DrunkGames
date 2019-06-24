<template>
  <div id="app">  
    <div class="bg"></div>  
    <MainPage v-show="mainPageShow" @SetPlayers="SetPlayers" :defaultCountPlayers="defaultCountPlayers"></MainPage>    
    <GamePanel v-show="gamePanelShow" @EndGame = "EndGame" :cards="cards" :players="players"></GamePanel>
    <EndGamePanel v-show="endGamePanelShow"></EndGamePanel>
    <b-modal id="modal-error" centered hide-header hide-footer>
      <h4>Заполните имена всех игроков</h4>
      <p class="my-4">Чтобы продолжить, заполни имена всех игроков</p>
      <b-button @click="$bvModal.hide('modal-error')" variant="outline-info">Извините, больше так не буду</b-button>
    </b-modal>
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import MainPage from './components/MainPage.vue'
import GamePanel from './components/GamePanel.vue'
import EndGamePanel from './components/EndGamePanel.vue'

import axios from 'axios'
import { clearInterval } from 'timers';

export default {
  name: 'app',
  components: {
    MainPage,
    GamePanel,
    EndGamePanel
  },
  data: function () {
    return {
      players: [],
      defaultCountPlayers: 2,
      currentCountPlayers: Number,
      cards: [{
        text: "",
        type: "",
        mode: 0,
      }],
      mainPageShow: true,
      gamePanelShow: false,
      endGamePanelShow: false,
      //reRender: 0,
    } 
  },
  methods: {
    
    SetPlayers: function(newPlayers, newCount) {
      //console.log(this)
      this.currentCountPlayers = newCount;
      this.players = newPlayers;
      //console.log(this.players)
      
      if (this.players.length == 0)
      {
        this.$bvModal.show("modal-error");
        return;
      }

      if (this.players.length - 1 == this.currentCountPlayers)
      {
        for (var i = 1; i < this.players.length; i++)
        {
          if (this.players[i] == "" || this.players[i] == null)
          {
            //console.log(this.players[0])
            this.$bvModal.show("modal-error");
            return;
          }          
        }
      }
      //this.reRender++;
      this.mainPageShow = false;      
      this.gamePanelShow = true;
      return;
    },
    EndGame: function () {
      this.gamePanelShow = false;
      this.endGamePanelShow = true;
    },
    SetCards: function (arrayCards) {
      arrayCards = arrayCards.sort(function () {return Math.random() -0.5});

      console.log("--------")
      console.log(arrayCards)
      console.log("--------")

      for (var i = 0; i < arrayCards.length; i++)
      {
        //console.log(i)     
        //console.log(arrayCards)   
        if (arrayCards[i].type === "virus")
        {
          var secondCard = Object.assign({}, arrayCards[i].secondCard);
          
          if (arrayCards.length - i > 5)
          {
            arrayCards.splice(this.RngInt(i+3, i + 5), 0, secondCard)
          }
          else
          {
            arrayCards.splice(arrayCards.length, 0, secondCard)
          }         
        }

        if (arrayCards[i].repeat != 0  && arrayCards[i].repeat != undefined)
        {
          var count = arrayCards[i].repeat - 1;
          arrayCards[i].repeat = 0;
          var secondCard = Object.assign({}, arrayCards[i]);
          
          for (var j = 0; j < count; j++)
          {
            //console.log(count);
            arrayCards.splice(this.RngInt(0, arrayCards.length), 0, secondCard);
          }
        }

        if (arrayCards[i].nextCard != undefined && arrayCards[i].nextCard != null)
        {
          arrayCards.splice(i + 1, 0, arrayCards[i].nextCard);
        }
      }

      return arrayCards;
    },
    RngInt: function(min, max) {
      var result = min + Math.floor(Math.random() * (max - min + 1));
      //console.log(result);
      return result; 
    },
  },
  mounted: function () {
    this.currentCountPlayers = this.defaultCountPlayers;
    //var self = this;
    axios.get('json/cards.json').then(responce => 
    { 
      this.cards = this.SetCards(responce.data.arrayCards); 
    })  
  }
}
</script>

<style>

@import url('https://fonts.googleapis.com/css?family=Lobster&display=swap&subset=cyrillic');
@import url('https://fonts.googleapis.com/css?family=El+Messiri:700&display=swap&subset=cyrillic');
@import url('https://fonts.googleapis.com/css?family=Rubik:400,500&display=swap&subset=cyrillic');

#app {
  /*font-family: 'Avenir', Helvetica, Arial, sans-serif;*/
  font-family: 'Rubik', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100vh;
  position: relative;
  
}

/*.bg
{
  height: 100vh;
  width: 100%;
  background: url("/img/bg.jpg") no-repeat;
  background-size: cover;
  filter: blur(5px);
  -webkit-filter: blur(5px);
  position: absolute;
  top: 0;
  left: 0;
  z-index: -1;
}*/

#modal-error
{
  text-align: center;
}

body
{
  height: 100vh;
  overflow: hidden;
  background: linear-gradient(#f5af19, #f12711)
  /*background: linear-gradient(#DA4453, #89216B);*/
  /*background: linear-gradient(#ff6a00, #ee0979)*/
  /*background: linear-gradient(#45B649,#acdc1a );*/
  /*background: linear-gradient(#9C27B0, #673AB7)*/
  /*background: linear-gradient(#f1c40f, #27ae60)*/
  /*background: #0288D1;*/
  /*background: #004b52;*/
  
}

.shadow
{
  box-shadow: 5px 5px 10px rgba(0,0,0,0.4)!important;
}
</style>
