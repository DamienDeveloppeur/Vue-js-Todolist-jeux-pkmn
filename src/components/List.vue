<template>
    <div id="List">
       <span>Votre nom : {{ data.name_dresseur }}</span><br>
        <div>Votre équipe</div>
        <ul>
            <li v-for="(pokemon, i) in team" :key="i">
                nom : {{pokemon.name}}
            </li>
        </ul>
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

</style>