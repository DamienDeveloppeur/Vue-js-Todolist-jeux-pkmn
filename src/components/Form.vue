<template>
 <div id="form">
   <img alt="Vue logo" src="../assets/prof-chen.png">
  <h1>Bien le bonjour !</h1>
  <h1>Bienvenue dans le monde magique des pokémons !</h1>
  <!-- <h2>Mon nom est CHEN ! Les gens souvent m'appellent le PROF POKEMON</h2>
  <h2>Ce monde est peuplé de créatures du nom de pokémon!</h2>
  <h2>Pour certains, les pokmémons sont des animaux domestiques, pour d'autres, ils sont un moyen de combattre</h2>
  <h2>Pour ma part ...</h2>
  <h2>L'étude des pokémon est ma profession</h2> -->
  <h1>Tout d'abord, quel est ton nom ?</h1>
  <p></p>
    <form id="form_name" @submit="checkForm">
        <p>
            <label for="name">Quel est ton prénom ?</label>
            <input v-model="name" type="text">
        </p>
        <p>
            <input type="submit" value="Submit">
        </p>
    </form>
 </div>
</template>
<script>
export default {
    name: "Form",
    data : function() {
      return {
        name: null,
      }
    },
    props : {data : Object},
    methods:{
      checkForm: function (e) {
        this.data.trainer.name_trainer = this.name;
        e.preventDefault();
      }
    }
}
</script>

<style scoped>
  #form_name p{
    display:flex;
    flex-direction: column;
    align-items: center;
  }
</style>