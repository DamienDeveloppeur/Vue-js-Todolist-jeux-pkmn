<template>
 <div id="form">
  <img alt="Vue logo" src="../assets/prof-chen.png">
  <h1>Maintenant, choisis un starter</h1>
  <p></p>
    <form id="starter">
        <p>
            <img key="1" src="../assets/carapuce.png" alt="" v-on:click="chooseStarter(pkmn[0])">
        </p>
        <p>
            <img src="../assets/salameche.png" alt="" v-on:click="chooseStarter(pkmn[1])">
        </p>
        <p>
            <img src="../assets/bulbizarre.png" alt="" v-on:click="chooseStarter(pkmn[2])">
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
      chooseStarter (p) {
        this.team.push(p)
        this.data.starter_name = p.name;
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