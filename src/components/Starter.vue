<template>
 <div id="form">
  <h1>Maintenant, choisis un starter</h1>
  <p></p>
    <form id="starter">
        <p>
            <label for="name">Carapuce</label>
            <img key="1" src="../assets/carapuce.png" alt="" v-on:click="chooseStarter(this.pkmn[0])">
        </p>
        <p>
            <label for="name">Salaméche</label>
            <img src="../assets/salameche.png" alt="" v-on:click="chooseStarter(this.pkmn[1])">
        </p>
        <p>
            <label for="name">Bulbizarre</label>
            <img src="../assets/bulbizarre.png" alt="" v-on:click="chooseStarter(this.pkmn[2])">
        </p>

    </form>
 </div>
</template>

<script>
export default {
    name: "Starter",
    data : function() {
      return {
        name: null,
      }
    },
    props : {data : Object,
            pkmn : Array,
            team : Array},
    methods:{
      chooseStarter (pokemon) {
        console.log(this.pkmn[0].name)
        this.team.push(pokemon)
       

      }
    }
}
</script>

<style scoped>
#starter{
    display : flex;
    justify-content:space-evenly;

}
#starter p {
    display:flex;
    flex-direction: column;
}
</style>