<template>
 <div id="city">
  <img :src="require(`@/assets/${this.data.localisation[this.data.actual_localisation].name}.png`)">
  <h1>Ville</h1>
  <h4>Vous pouvez soigner vos pokémon ou acheter des objets en boutiques</h4>
  <button @click="fullHeal">Soigner vos pokémons au centre</button>
  <button>Visiter une boutique</button>
 </div>
</template>
p
<script>
export default {
    name: "City",
    data : function() {
      return {
        name: null,
      }
    },
    props : {
      data : Object,
      team : Array,
    },
    methods:{
      fullHeal : function() {
        for (let i in this.team) {
          this.team[i].current_stat.pv = this.team[i].base_stat.pv;
        }
      }

    }
}
</script>

<style scoped>

</style>