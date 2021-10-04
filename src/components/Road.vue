<template>
 <div id="city">
   <img alt="Vue logo" src="../assets/road.png">
  <h1>Route</h1>
  <h2>Un pokémon sauvage vous attaque !</h2>
  <p>{{foePkmn}}</p>
    <div class="thumbnail-pkmn">
        <div class="entry">
            <div class="test">
                <span>Nom : </span> <span>{{foePkmn.name}}</span>
            </div>
            <div class="test">
                <div class="barre_exp">
                    <div class="stat_hp" :style="{ width: foePkmn.current_stat.pv  * 200 / foePkmn.base_stat.pv + 'px' }">
                    </div>
                </div>
                <!-- <span>Pv : </span> <span>{{pokemon.pv}}</span> -->
            </div>
        </div>
    </div>
    <h3>Dans cette version, vous ne pouvez fuir (bah oui gros lache)</h3>
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
            this.foePkmn =  {name: 'salaméche', id: 3, ability : [ {name: "charge", damage : 5}], base_stat : {pv : 50, atk : 5, def:6}, curent_stat : {pv : 50, atk : 5, def:6}},

            console.log(this.foePkmn);
        }
    },
    beforeMount(){
        this.foePkmnAttak()
    },
}
</script>

<style scoped>

</style>