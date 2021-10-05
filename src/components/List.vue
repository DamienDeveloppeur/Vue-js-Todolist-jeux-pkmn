<template>
    <div id="List">
        <div>Votre équipe</div>
        <ul>
            <li class="thumbnail-pkmn" v-for="(pokemon, i) in team" :key="i">
                <div class="entry">
                    <div class="column">
                        <div><span>Nom : </span> <span>{{pokemon.name}}</span></div> 
                        <div><span>Niveaux : </span> <span>{{pokemon.level}}</span></div>
                    </div>
                    <div class="stat">
                        <div class="barre_exp">
                            <div class="stat_hp" :style="{ width: pokemon.current_stat.pv  * 200 / pokemon.base_stat.pv + 'px' }">
                            </div>
                        </div>
                        <div class="barre_exp">
                            <div class="stat_exp" :style="{ width: pokemon.current_stat.exp * 2+ 'px' }">
                            </div>
                        </div>
                        <!-- <span>Pv : </span> <span>{{pokemon.pv}}</span> -->
                    </div>
                    <div class="stat">
                        <li v-for="(attack, i) in pokemon.ability" :key="i">
                           <div @click="atk(attack)">{{attack.name}}</div> 
                           
                        </li>
                    </div>
                </div>
            </li>
        </ul>
        <div class="stat_dresseur">
            <div class="localisation">
                Votre localisation : {{this.data.localisation[this.data.actual_localisation].name}}
            </div>
            <div class="nom">
                <div>Votre nom : {{data.trainer.name_trainer }}</div><br>
            </div>
            <div class="bag">
                <div>Montant pokedollar : {{this.data.trainer.pokedollar}}</div>
                <button>Voir le contenu du sac</button>
            </div>
            <div class="hungry">
                    <div class="barre_exp">
                        <div class="stat_hungry" :style="{ width: data.trainer.stat_hungry * 2+ 'px' }">

                        </div>
                    </div>
            </div>
        
        </div>


    </div>
</template>

<script>
export default {
    name: 'List', 
    props : {data : Object,
    team : Array,
    pkmn : Array},
    methods : {
        displayStat: function () {
            console.log(this.pkmn[0].ability)
        },
         atk : function (a) {
          this.$emit("attack",a);
        },
    },
    beforeMount(){
        this.displayStat();
    },
}
</script>

<style>
.stat {
    display: flex;
    flex-direction: column;
    align-items: center;
}
.thumbnail-pkmn {
    display:flex;
    border:1px solid black;
    max-width:50%;
}
.entry {
    width: 100%; 
    /* display:flex;
    justify-content: space-evenly; */
}
.mini_barre_exp {
    width:100px;
    height:24px;
    border :1px solid black;
}
.barre_exp {
    animation: 3s linear 1s slidein;
    width:200px;
    height:24px;
    border :1px solid black;
}
.stat_dresseur {
    display: flex;
    flex-direction: column;
    align-items: center;
}
.stat_hp {
    height:100%;
    /* width: 0px; */
    background-color:red;
}
.stat_exp {
    height:100%;
    background-color:blue;
}
.stat_hungry {
    height:100%;
    background-color:green;
}
</style>