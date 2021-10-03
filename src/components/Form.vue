<template>
 <div id="form">
   <img alt="Vue logo" src="../assets/prof-chen.png">
  <h1>Bienvenue dans le monde des pokémons !</h1>
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
        // console.log(this.data)
        this.data.name_dresseur = this.name;

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