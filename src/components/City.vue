<template>
 <div id="city">
   <img alt="Vue logo" src="../assets/city.png">
  <h1>Ville</h1>
  <p></p>
 </div>
</template>

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