<template>
 <div id="form">
   <img alt="Vue logo" src="../assets/prof-chen.png">
  <h1>Bienvenue dans le monde des pokémons !</h1>
  <p>Dans cete run, vous aurez une stat de faim qui baissera au fur et à mesure de votre aventure</p>
  <p>Vous devriez combatre pour gagner des pokédollar, pour pouvoir acheter de la nouriture</p>
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
        console.log(this.data.trainer.name_trainer)
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