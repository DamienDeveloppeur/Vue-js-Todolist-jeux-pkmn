<template>
 <div id="road">
   <img class="city-road-img" :src="require(`@/assets/${this.data.localisation[this.data.actual_localisation].name}.png`)">
  <h1>Route</h1>
  <h2>Un pokémon sauvage vous attaque !</h2>
    <Foepkmn v-bind:data="data" :team="team" :pkmn="pkmn"></Foepkmn>
    <h3>Vous devez vaincre le pkmn sauvage pour pouvoir continuer</h3>
  <h3 v-if="data.foePkmn.status">{{data.turn ? "Votre tour" : "Tour de du pokémon sauvage"}}</h3> 
  <h3 v-if="!data.foePkmn.status">Bravo, vous avez vaincu ce {{data.foePkmn.name}} sauvage </h3>
 </div>
</template>

<script>
import Foepkmn from '../components/Foepkmn.vue'

export default {
    name: "Road",
    data : function() {
      return {
        foePkmn: null,
      }
    },
    props : {data : Object,
    team : Array,
    pkmn : Array},
    methods:{
    },
    components: {
        Foepkmn
    },
    // beforeMount(){
    //     this.foePkmnAttak()
    // },
}
</script>

<style scoped>
.city-road-img {
  width: 350px;
  height:350px;
}
</style>