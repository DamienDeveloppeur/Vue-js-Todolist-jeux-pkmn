<template>
 <div id="city">
   <img alt="Vue logo" src="../assets/city.png">
  <h1>Ville</h1>
  <h4>Vous pouvez soigner vos pokémon ou acheter des objets en boutiques</h4>


  <button>Soigner vos pokémons au centre</button>
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
    props : {data : Object},
    methods:{

    }
}
</script>

<style scoped>

</style>