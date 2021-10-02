<template>
 <div id="form">
  <h1>Bienvenue dans le monde des pokémons !</h1>
  <p></p>
    <form @submit="checkForm">
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
    props : {data : Object,
    team : Array},
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

</style>