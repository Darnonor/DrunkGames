<template>
  <div id="app">    
    <MainPage @SetPlayers="SetPlayers" :defaultCountPlayers="defaultCountPlayers"></MainPage>
    

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

export default {
  name: 'app',
  components: {
    MainPage
  },
  data: function () {
    return {
      players: Array,
      defaultCountPlayers: 2,
      currentCountPlayers: Number,
    } 
  },
  methods: {
    SetPlayers: function(newPlayers, newCount) {
      //if (newPlayers)
      this.currentCountPlayers = newCount;
      console.log(newPlayers)
      if (newPlayers.length - 1 == this.currentCountPlayers)
      {
        for (var i = 0; i < newPlayers.length - 1; i++)
        {
          if (newPlayers[i] == "" || newPlayers[i] == null)
          {
            this.$bvModal.show("modal-error");
            return;
          }
          
        }
      }
      else
      {
        this.$bvModal.show("modal-error");
        return;
      }


      this.players = newPlayers;
      
    }
  },
  mounted: function () {
    this.currentCountPlayers = this.defaultCountPlayers;
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
}

#modal-error
{
  text-align: center;
}

body
{
  height: 100vh;
  overflow: hidden;
  /*background: linear-gradient(#f5af19, #f12711)*/
  /*background: linear-gradient(#DA4453, #89216B);*/
  /*background: linear-gradient(#ff6a00, #ee0979)*/
  /*background: linear-gradient(#45B649,#acdc1a );*/
  /*background: linear-gradient(#5691c8, #457fca)*/
  background: linear-gradient(#f1c40f, #27ae60)
}
</style>
