<template>
    <div id="List">
       <span>Votre nom : {{ data.name_dresseur }}</span><br>
        <div>Votre équipe</div>
        <ul>
            <li class="thumbnail-pkmn" v-for="(pokemon, i) in team" :key="i">
                <div class="entry">
                    <div class="test">
                        <span>Nom : </span> <span>{{pokemon.name}}</span>
                    </div>
                    <div class="test">
                        <div class="barre_exp">
                            <div class="stat_hp" :style="{ width: pokemon.current_stat.pv  * 200 / pokemon.base_stat.pv + 'px' }">
                            </div>
                        </div>
                        <!-- <span>Pv : </span> <span>{{pokemon.pv}}</span> -->
                    </div>
                    <div class="test">
                        <li v-for="(attack, i) in pokemon.ability" :key="i">
                           <div v-on:click="this.attack(attack.name)">{{attack.name}}</div> 
                        </li>
                    </div>
                </div>
            </li>
        </ul>
        <div class="localisation">
            Votre localisation : {{this.data.localisation[this.data.actual_localisation].name}}
        </div>

    </div>
</template>

<script>
export default {
    name: 'List', 
    props : {data : Object,
    team : Array},
    methods : {
       
    },

}
</script>

<style>
.test {
    display: flex;
    justify-content: center;
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
.stat_hp {
    height:100%;
    /* width: 0px; */
    background-color:red;
}
</style>