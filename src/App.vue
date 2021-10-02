<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/prof-chen.png">
     <!--  -->
    <Form v-bind:data="data" v-if="!this.data.name_dresseur"/>
    <Starter v-bind:data="data" :pkmn="pkmn" :team="team" v-if="!this.data.starter_name&&this.data.name_dresseur"></Starter>
    <List v-bind:data="data" :team="team" />
  </div>
</template>

<script>
import Form from './components/Form.vue'
import List from './components/List.vue'
import Starter from './components/Starter.vue'

export default {
  name: 'App',
  data : function() {
    return {
      pkmn: [
          {name: 'carapuce', id: 1, pv :50,atk : 5, def : 6},
          {name: 'bulbizarre', id: 2, pv:55, atk:4, def:7},
          {name: 'salaméche', id: 3, pv:45, atk : 6, def:5},
      ],
      data : {
        name_dresseur : "",
        name_pkmn : "",
        starter_name : "",
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
    Starter
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
