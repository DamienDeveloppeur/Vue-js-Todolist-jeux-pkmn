<template>
 <div id="city">
  <img :src="require(`@/assets/${this.data.localisation[this.data.actual_localisation].name}.png`)">
  <h1>Ville</h1>
  <h4>Vous pouvez soigner vos pokémon ou acheter des objets en boutiques</h4>
  <button @click="fullHeal">Soigner vos pokémons au centre</button>
  <button @click="visitShop">{{ shop ? "Sortir de la boutique" : "Enrer dans la boutique"}}</button>
    <div v-if="shop" id="shop">
      <div class="article_traier">
        <div v-for="(p,i) in data.product_shop" :key="i">
         <button @click="buyProduct(p)">{{p.name}} : {{p.price}}$ </button>
        </div>
      </div>
      <div class="article_pkmn">

      </div>
    </div>
 </div>
</template>
p
<script>
export default {
    name: "City",
    data : function() {
      return {
        name: null,
        shop:false,
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
      },
      visitShop : function(){
        this.shop ? this.shop = false : this.shop = true;
      },
      buyProduct: function (p) {
        this.data.trainer.bag.push(p)
        if(this.data.trainer.pokedollar >= p.price) {
          this.data.trainer.pokedollar -= p.price;
          console.log(this.data.trainer.bag)
        }

      },
    }
}
</script>

<style scoped>

</style>