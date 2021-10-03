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
                        <span>Pv : </span> <span>{{pokemon.pv}}</span>
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
        del_func: function (index) {
            this.items.splice(index, 1);
        },
        acomplished: function (index) {
            this.items[index].done = true;
        }
    }
}
</script>

<style>
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
</style>