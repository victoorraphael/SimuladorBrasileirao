<template>
  <div id="app">    

    <Header part1="Simulador do " part2="Brasileirão 2020"/>

    <SubHeader texto="Simule os resultados dos jogos do Brasileirão 2020, 
                    e tente adivinhar o campeão, quais times vão à Libertadores e à 
                    Copa Sul-Americana e quem será rebaixado para a Série B"/>

    <div class="containers">
      
      <div class="container-ranking">
        
        <Ranking title="Tabela" :teams="championship.teams" />

      </div>

      <div class="container-games">
        <Rounds title="Rodadas" 
                :round="round"
                @navigate="navigate" />
      </div>

    </div>    

  </div>
</template>

<script>

// Components
import Header from './components/Header.vue';
import SubHeader from './components/SubHeader.vue';
import Ranking from './components/Ranking.vue';
import Rounds from './components/Rounds.vue';

// Services
import Championship from './models/championship.js'

export default {
  name: 'App',
  
  components: {
    Header, SubHeader,
    Ranking, Rounds
  },

  data(){
    return {
      championship: null,
      round: null
    }
  },

  methods: {

      navigate: function(type){

          if ( type == 'prev'){
            this.round = this.championship.prevRound()

          }else if ( type == 'next') {
            this.round = this.championship.nextRound()
          }
          
      }
  },

  beforeMount(){
      this.championship = Championship.new()
      this.round = this.championship.currentRound()
  }

}
</script>

<style>

@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;900&display=swap');

*{
  padding:0;
  margin:0;
}

#app {
  font-family: 'Roboto', sans-serif;
  width:95%;
  margin:0 auto;
}

.containers{
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  margin:50px auto;
  height:400px;
}

.container-ranking{
  width:55%;
  display:flex;
  flex-direction: column;
}

.container-games{
  width:40%;
}

</style>
