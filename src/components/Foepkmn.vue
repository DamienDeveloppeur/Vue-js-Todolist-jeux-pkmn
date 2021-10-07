<template>
 <div id="foePkmn">
    <div class="thumbnail-pkmn">
        <div class="entry">
            <div class="column">
                <div><span>Nom : </span><span>{{this.data.foePkmn.name}}</span></div> 
                <div><span>Niveaux : </span><span>{{this.data.foePkmn.level}}</span></div> 
                <div class="center">
                    <div class="barre_exp">
                        <div class="stat_hp" :style="{ width: this.data.foePkmn.current_stat.pv  * 200 / this.data.foePkmn.base_stat.pv + 'px' }">
                        </div>
                    </div>
                </div> 
            </div>
        </div>
    </div>
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
.center {
    display: flex;
    justify-content: center;
}
</style>