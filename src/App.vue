<template>
  <div id="app">
    <Form v-bind:data="data" v-if="!this.data.name_dresseur"/>
    <Starter v-bind:data="data" :pkmn="pkmn" :team="team" v-if="!this.data.starter_name&&this.data.name_dresseur"></Starter>
    <City v-if="this.data.localisation[this.data.actual_localisation].type === 'city'&&this.data.starter_name"></City>
    <Road v-bind:data="data" :pkmn="pkmn" :team="team" v-if="this.data.localisation[this.data.actual_localisation].type === 'road'&&this.data.starter_name"></Road>
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
            ability : [ {name: "charge", damage : 5}],
            base_stat : {pv : 50, atk : 5, def:6},
            current_stat : {pv : 50, atk : 5, def:6},
            status : true
          },
          {
            name: 'salaméche', 
            id: 3, 
            ability : [ {name: "charge", damage : 5}], 
            base_stat : {pv : 50, atk : 5, def:6}, 
            current_stat : {pv : 50, atk : 5, def:6},
            status : true
          },
          {
            name: 'bulbizarre', 
            id: 2, 
            ability : [ {name: "charge", damage : 5}], 
            base_stat : {pv : 50, atk : 5, def:6}, 
            current_stat : {pv : 50, atk : 5, def:6},
            status : true
          },
      ],
      data : {
        name_dresseur : "",
        name_pkmn : "",
        starter_name : "",
        localisation : [
          {name: "bourg palette", id: 0, type: "city"},
          {name: "route 1", id : 0, type: "road"},
          {name: "jadielle", id : 0, type: "city"},

        ],
        actual_localisation : 0,
        foePkmn : {},
        turn : true,
        
      },
      team : [
        
      ],
      config : {
        
      },
    }
  },
  methods : {
    attacks : function (a) {
      if(this.data.turn) {
        let attacker = this.team[0], defender = this.data.foePkmn;
        console.log(attacker, defender)
        this.data.turn = false;
      } else {
        let attacker = this.data.foePkmn, defender = this.team[0];
        console.log(attacker, defender)
        this.data.turn = true;
      }
      // faire baisser les pv du defender en fonction de l'attaque de l'attacker 
      this.data.foePkmn.current_stat.pv -= a.damage;
      if(this.data.foePkmn.current_stat.pv <= 0) this.data.foePkmn.status = false;
    }
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
