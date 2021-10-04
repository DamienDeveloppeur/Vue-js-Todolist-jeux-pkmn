<template>
 <div id="city">
   <img alt="Vue logo" src="../assets/road.png">
  <h1>Route</h1>
  <h2>Un pokémon sauvage vous attaque !</h2>
  <p>{{this.data.foePkmn}}</p>
    <div class="thumbnail-pkmn">
        <div class="entry">
            <div class="test">
                <span>Nom : </span> <span>{{this.data.foePkmn.name}}</span>
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
                                    name: 'salaméche', 
                                    id: 3, 
                                    ability : [ {name: "charge", damage : 5}], 
                                    base_stat : {pv : 50, atk : 5, def:6}, 
                                    current_stat : {pv : 50, atk : 5, def:6},
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