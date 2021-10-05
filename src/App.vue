<template>
  <div id="app">
    <Form v-bind:data="data" v-if="!this.data.trainer.name_trainer"/>
    <Starter v-bind:data="data" :pkmn="pkmn" :team="team" v-if="!this.data.starter_name&&this.data.trainer.name_trainer"></Starter>
    <City v-if="this.data.localisation[this.data.actual_localisation].type === 'city'&&this.data.starter_name" v-bind:data="data" :team="team" ></City>
    <Road v-bind:data="data" :team="team" :pkmn="pkmn"  v-if="this.data.localisation[this.data.actual_localisation].type === 'road'&&this.data.starter_name"></Road>
    <Map v-bind:data="data" v-if="this.data.starter_name"></Map>
    <List v-bind:data="data" :team="team" :pkmn="pkmn" @attack="attacks" />
  
  </div>
</template>

<script>
import Form from './components/Form.vue'
import List from './components/List.vue'
import Starter from './components/Starter.vue'
import Map from './components/Map.vue'
import City from './components/City.vue'
import Road from './components/Road.vue'

export default {
  name: 'App',
  data : function() {
    return {
      pkmn: [
          {
            name: 'carapuce', 
            id: 1,
            level : 1,
            ability : [ {name: "charge", damage : 5}],
            base_stat : {pv : 50, atk : 5, def:6},
            current_stat : {pv : 50, atk : 5, def:6,exp : 0,},
            status : true
          },
          {
            name: 'salaméche', 
            id: 3, 
            level : 1,
            ability : [ {name: "charge", damage : 5}], 
            base_stat : {pv : 50, atk : 5, def:6}, 
            current_stat : {pv : 50, atk : 5, def:6,exp : 0},
            status : true
          },
          {
            name: 'bulbizarre', 
            id: 2, 
            level : 1,
            ability : [ {name: "charge", damage : 5}], 
            base_stat : {pv : 50, atk : 5, def:6}, 
            current_stat : {pv : 50, atk : 5, def:6,exp : 0},
            status : true
          },
      ],
      data : {
        name_pkmn : "",
        starter_name : "",
        localisation : [
          {name: "bourg-palette", id: 1, type: "city"},
          {name: "route-1", id : 2, type: "road"},
          {name: "jadielle", id : 3, type: "city"},
        ],
        actual_localisation : 0,
        foePkmn : {},
        turn : true,
        trainer : {
          name_trainer : "",
          stat_hungry : 100,
          bag : {},
          pokedollar : 50,
        },
        game_over : false
        
      },
      team : [
        
      ],
      config : {
        
      },
    }
  },
  methods : {
    attacks : function (a) {
      if(this.data.turn && this.team[0].status) {
        this.data.foePkmn.current_stat.pv -= a.damage;
        if(this.data.foePkmn.current_stat.pv <= 0){
          this.data.foePkmn.status = false; 
          this.data.turn = true;
          this.team[0].current_stat.exp += 25;
          if(this.team[0].current_stat.exp >= 100) {
            this.team[0].level +=1;
            this.team[0].current_stat.exp = this.team[0].current_stat.exp - 100;
          }
          return;
        } 
        else this.data.turn = false;
        this.attacks(this.data.foePkmn.ability[0]);
      } else if (!this.data.turn && this.team[0].status) {
        setInterval(() => {
          if (!this.data.turn && this.data.foePkmn.status) {
            this.team[0].current_stat.pv -= this.data.foePkmn.ability[0].damage;
            if(this.team[0].current_stat.pv <= 0) this.team[0].status = false;
            this.data.turn = true;
          }
        }, 1000)
      }
      // faire baisser les pv du defender en fonction de l'attaque de l'attacker 
    },
    startHungry: function (){
      setInterval(() => {
        this.data.trainer.stat_hungry--;
      },2000)
    }

  },
  beforeMount(){
    this.startHungry();
  },
  components: {
    Form,
    List,
    Starter,
    Map,
    City,
    Road
  },
   
}
// console.log(this.items);
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
