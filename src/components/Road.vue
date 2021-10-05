<template>
 <div id="road">
   <img :src="require(`@/assets/${this.data.localisation[this.data.actual_localisation].name}.png`)">
  <h1>Route</h1>
  <h2>Un pokémon sauvage vous attaque !</h2>
  <p>{{this.data.foePkmn}}</p>
    <div class="thumbnail-pkmn">
        <div class="entry">
            <div class="column">
                <div><span>Nom : </span> <span>{{this.data.foePkmn.name}}</span></div> 
                <div><span>Niveaux : </span> <span>{{this.data.foePkmn.level}}</span></div>  
            </div>
            <div class="test">
                <div class="barre_exp">
                    <div class="stat_hp" :style="{ width: this.data.foePkmn.current_stat.pv  * 200 / this.data.foePkmn.base_stat.pv + 'px' }">
                    </div>
                </div>
                <!-- <span>Pv : </span> <span>{{pokemon.pv}}</span> -->
            </div>
            <div class="capComba">

            </div>
        </div>
    </div>
    <h3>Vous devez vaincre le pkmn sauvage pour pouvoir continuer</h3>
  <h3 v-if="data.foePkmn.status">{{data.turn ? "Votre tour" : "Tour de du pokémon sauvage"}}</h3> 
  <h3 v-if="!data.foePkmn.status">Bravo, vous avez vaincu ce {{data.foePkmn.name}} sauvage </h3>
 </div>
</template>

<script>
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
        foePkmnAttak() {
            // select foe pkmn
            this.data.foePkmn = {
                                    name: 'miaous', 
                                    id: 3, 
                                    level : 1,
                                    ability : [
                                        {name: "griffe", damage : 5, target : "pv", type : "degat"}
                                    ], 
                                    base_stat : {pv : 40, atk : 5, def:4}, 
                                    current_stat : {pv : 40, atk : 5, def:4},
                                    status : true
                            };
        
        },
    },
    beforeMount(){
        this.foePkmnAttak()
    },
}
</script>

<style scoped>
.capComba {
    
}
</style>