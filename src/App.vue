<template>
  <div id="app">
    <Form v-bind:data="data" v-if="!this.data.trainer.name_trainer"/>
    <Starter v-bind:data="data" :pkmn="pkmn" :team="team" v-if="!this.data.starter_name&&this.data.trainer.name_trainer"></Starter>
    <City v-if="this.data.localisation[this.data.actual_localisation].type === 'city'&&this.data.starter_name" v-bind:data="data" :team="team" ></City>
    <Road v-bind:data="data" :team="team" :pkmn="pkmn"  v-if="this.data.localisation[this.data.actual_localisation].type === 'road'&&this.data.starter_name"></Road>
    <Map v-bind:data="data" v-if="this.data.starter_name" @foePkmnComming="foePkmnComming"></Map>
    <List v-bind:data="data" :team="team" :pkmn="pkmn" @attack="attacks" />
    <!-- {{meteo}}
    {{meteo.name}} -->
      <h3>Météo</h3>
            <p>Ville: {{ meteo.name }}</p>
            <p>Humidité: {{ meteo.main.humidity }}%</p>
            <p>Vent: {{ meteo.wind.speed }}m/s</p>

  </div>
</template>
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<script>
import Form from './components/Form.vue'
import List from './components/List.vue'
import Starter from './components/Starter.vue'
import Map from './components/Map.vue'
import City from './components/City.vue'
import Road from './components/Road.vue'
import axios from 'axios'

export default {
  name: 'App',
  data : function() {
    return {
      pkmn: [
          {
            name: 'carapuce', 
            id: 1,
            level : 1,
            ability : [ 
              {name: "charge", damage : 5, target : "pv", type : "degat"},
              {name : "gros-yeux", damage: 4,target : "def", type: "support"}
              ],
            base_stat : {pv : 50, atk : 5, def:6},
            current_stat : {pv : 50, atk : 5, def:6},
            exp : 0,
            status : true
          },
          {
            name: 'salaméche', 
            id: 3, 
            level : 1,
            ability : [
              {name: "griffe", damage : 5, target : "pv", type : "degat"},
              {name : "gros-yeux", damage: 5,target : "def", type: "support"}
            ], 
            base_stat : {pv : 50, atk : 5, def:6}, 
            current_stat : {pv : 50, atk : 5, def:6},
            exp : 0,
            status : true
          },
          {
            name: 'bulbizarre', 
            id: 2, 
            level : 1,
            ability : [
              {name: "charge", damage : 5, target : "pv", type : "degat"},
              {name : "mimi-queue", damage: 5,target : "def", type: "support"}
            ], 
            base_stat : {pv : 50, atk : 5, def:6}, 
            current_stat : {pv : 50, atk : 5, def:6},
            exp : 0,
            status : true
          },
      ],
      data : {
        name_pkmn : "",
        starter_name : "",
        localisation : [
          {name: "bourg-palette", id: 1, type: "city"},
          {name: "route-1", id : 2, type: "road"},
          {name: "jadielle", id : 3, type: "city"},
          {name: "route-2", id : 4, type: "road"},
          {name: "foret-de-jade", id : 5, type: "road"},
          {name: "argenta", id : 6, type: "city"},
        ],
        actual_localisation : 0,
        foePkmn : {},
        turn : true,
        trainer : {
          name_trainer : "",
          stat_hungry : 100,
          bag : [],
          pokedollar : 50,
        },
        product_shop : [
          {name : "food", price : 25, effect : "eat"},
          {name: "pokeball", price : 20, effect : 'capture'}
        ],
        game_over : false,
        
      },
      team : [
        
      ],
      meteo : {
        
      },
    }
  },
  methods : {
    attacks : function (a) {
      if(this.data.turn && this.team[0].status) {
        if(a.target == "pv") {
          let additionnalDamage = this.team[0].current_stat.atk - this.data.foePkmn.current_stat.def 
          if (additionnalDamage <= 0) this.data.foePkmn.current_stat.pv--;
          else this.data.foePkmn.current_stat.pv -= a.damage + additionnalDamage;
        } 
        else this.data.foePkmn.current_stat.def -= a.damage;
        if(this.data.foePkmn.current_stat.pv <= 0){
          this.data.foePkmn.current_stat.pv = 0;
          this.data.foePkmn.status = false; 
          this.data.turn = true;
          this.leveling();
          this.data.trainer.pokedollar += 25;
          return;
        } 
        else this.data.turn = false;
        this.attacks(this.data.foePkmn.ability[0]);
      } else if (!this.data.turn && this.team[0].status) {
        setInterval(() => {
          if (!this.data.turn && this.data.foePkmn.status) {
            this.team[0].current_stat.pv -= this.data.foePkmn.ability[0].damage;
            // if(this.team[0].current_stat.pv <= 0) this.team[0].status = false;
            this.data.turn = true;
          }
        }, 1000)
      }
    },
    foePkmnComming : function (){
      // select foe pkmn
      this.data.foePkmn = {
          name: 'miaous', 
          id: 4, 
          level : 1,
          ability : [
              {name: "griffe", damage : 5, target : "pv", type : "degat"}
          ], 
          base_stat : {pv : 40, atk : 3, def:4}, 
          current_stat : {pv : 40, atk : 3, def:4},
          status : true
      };
        
    },
    startHungry: function (){
      setInterval(() => {
        this.data.trainer.stat_hungry--;
      },2000)
    },
    leveling : function (){
        for (let i in this.team[0].base_stat) {
          this.team[0].base_stat[i] += 2;
          this.team[0].current_stat[i] += 2;
        }
        this.team[0].exp += 25;
        if(this.team[0].exp >= 100) {
          this.team[0].level +=1;
          this.team[0].exp = this.team[0].exp - 100;
    
        }
    },
    apiMeteo : function (){
      // setTimeout(function(){


      // }, 500);
          // Make a request for a user with a given ID
      axios.get('https://api.openweathermap.org/data/2.5/weather?q=montpellier&appid=dced8c7e19301276fcf28e033a299134')
      .then( (r) => {
       this.meteo = r.data
      })
      .catch(function (error) {
          console.log(error);
      })
      .then(function () {
      });
    }
  },
  beforeMount(){
    this.startHungry();
    
    this.apiMeteo();
  },
  components: {
    Form,
    List,
    Starter,
    Map,
    City,
    Road
  },
   
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.btn {
  flex: 1 1 auto;
  margin: 10px;
  padding: 30px;
  text-align: center;
  text-transform: uppercase;
  transition: 0.5s;
  background-size: 200% auto;
  color: white;
 /* text-shadow: 0px 0px 10px rgba(0,0,0,0.2);*/
  box-shadow: 0 0 20px #eee;
  border-radius: 10px;
 }

.btn:hover {
  background-position: right center; /* change the direction of the change here */
}

.btn-1 {
  background-image: linear-gradient(to right, #f6d365 0%, #fda085 51%, #f6d365 100%);
}

.btn-2 {
  background-image: linear-gradient(to right, #fbc2eb 0%, #a6c1ee 51%, #fbc2eb 100%);
}

.btn-3 {
  background-image: linear-gradient(to right, #84fab0 0%, #8fd3f4 51%, #84fab0 100%);
}

.btn-4 {
  background-image: linear-gradient(to right, #a1c4fd 0%, #c2e9fb 51%, #a1c4fd 100%);
}

.btn-5 {
  background-image: linear-gradient(to right, #ffecd2 0%, #fcb69f 51%, #ffecd2 100%);
}
</style>
