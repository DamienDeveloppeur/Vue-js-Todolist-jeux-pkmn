<template>
  <div id="app">
    <Form v-bind:data="data" v-if="!this.data.name_dresseur"/>
    <Starter v-bind:data="data" :pkmn="pkmn" :team="team" v-if="!this.data.starter_name&&this.data.name_dresseur"></Starter>
    <Map v-bind:data="data" v-if="this.data.starter_name"></Map>
    <List v-bind:data="data" :team="team" />
    
  </div>
</template>

<script>
import Form from './components/Form.vue'
import List from './components/List.vue'
import Starter from './components/Starter.vue'
import Map from './components/Map.vue'

export default {
  name: 'App',
  data : function() {
    return {
      pkmn: [
          {name: 'carapuce', id: 1, pv :50,atk : 5, def : 6, ability : [ {name: "charge", damage : 5}]},
          {name: 'salaméche', id: 3, pv:45, atk : 6, def:5, ability : [ {name: "charge", damage : 5}]},
          {name: 'bulbizarre', id: 2, pv:55, atk:4, def:7, ability : [ {name: "charge", damage : 5}]},
      ],
      data : {
        name_dresseur : "",
        name_pkmn : "",
        starter_name : "",
        localisation : [
          {name: "bourg palette", id: 0, type: "ville"},
          {name: "route 1", id : 0, type: "route"},
          {name: "jadielle", id : 0, type: "ville"},

        ],
        actual_localisation : 0,
        
      },
      team : [
        
      ],
      config : {
        
      },
    }
  },
  components: {
    Form,
    List,
    Starter,
    Map
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
