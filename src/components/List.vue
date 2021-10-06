<template>
    <div id="List">
        <div>Votre équipe</div>
        <!-- flip-card-container -->
        <div id="team_pkmn" class="flip-card-container" style="--hue: 220">
            <div class="flip-card">
                <div class="card-front">
                <figure>
                    <div class="img-bg"></div>
                    <img src="../assets/logo-pkmn.jpg" alt="Brohm Lake">
                    <!-- <img src="https://images.unsplash.com/photo-1486162928267-e6274cb3106f?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=500&q=60" alt="Brohm Lake"> -->
                    <figcaption>Brohm Lake</figcaption>
                </figure>

                <ul>
                    <li>Detail 1</li>
                    <li>Detail 2</li>
                    <li>Detail 3</li>
                    <li>Detail 4</li>
                    <li>Detail 5</li>
                </ul>
                </div>

                <div class="card-back">
                <figure>
                    <div class="img-bg"></div>
                    <img src="https://images.unsplash.com/photo-1486162928267-e6274cb3106f?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=500&q=60" alt="Brohm Lake">
                </figure>

                <button>Book</button>

                <div class="design-container">
                    <span class="design design--1"></span>
                    <span class="design design--2"></span>
                    <span class="design design--3"></span>
                    <span class="design design--4"></span>
                    <span class="design design--5"></span>
                    <span class="design design--6"></span>
                    <span class="design design--7"></span>
                    <span class="design design--8"></span>
                </div>
                </div>

            </div>
        </div>
<!-- /flip-card-container -->

  <!-- flip-card-container -->
        <div id="bag" class="flip-card-container" style="--hue: 220">
            <div class="flip-card">
                <div class="card-front">
                <figure>
                    <div class="img-bg"></div>
                    <img src="../assets/logo-pkmn.jpg" alt="Brohm Lake">
                    <!-- <img src="https://images.unsplash.com/photo-1486162928267-e6274cb3106f?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=500&q=60" alt="Brohm Lake"> -->
                    <figcaption>Brohm Lake</figcaption>
                </figure>

                <ul>
                    <li>Detail 1</li>
                    <li>Detail 2</li>
                    <li>Detail 3</li>
                    <li>Detail 4</li>
                    <li>Detail 5</li>
                </ul>
                </div>

                <div class="card-back">
                <figure>
                    <div class="img-bg"></div>
                    <img src="https://images.unsplash.com/photo-1486162928267-e6274cb3106f?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=500&q=60" alt="Brohm Lake">
                </figure>

                <button>Book</button>

                <div class="design-container">
                    <span class="design design--1"></span>
                    <span class="design design--2"></span>
                    <span class="design design--3"></span>
                    <span class="design design--4"></span>
                    <span class="design design--5"></span>
                    <span class="design design--6"></span>
                    <span class="design design--7"></span>
                    <span class="design design--8"></span>
                </div>
                </div>

            </div>
        </div>
<!-- /flip-card-container -->
        <div>
            <div class="thumbnail-pkmn" v-for="(pokemon, i) in team" :key="i">
                <div class="entry">
                    <div class="column">
                        <div><span>Nom : </span> <span>{{pokemon.name}}</span></div> 
                        <div><span>Niveaux : </span> <span>{{pokemon.level}}</span></div>
                    </div>
                    <div class="stat">
                        <div class="barre_exp">
                            <div class="stat_hp" :style="{ width: pokemon.current_stat.pv  * 200 / pokemon.base_stat.pv + 'px' }">
                            </div>
                        </div>
                        <div class="barre_exp">
                            <div class="stat_exp" :style="{  width: pokemon.current_stat.exp * 2+ 'px' }">
                            </div>
                        </div>
                        <!-- <span>Pv : </span> <span>{{pokemon.pv}}</span> -->
                    </div>
                    <div class="stat" v-if="data.foePkmn.status">
                        <li v-for="(attack, i) in pokemon.ability" :key="i">
                           <div @click="atk(attack)">{{attack.name}}</div> 
                        </li>
                    </div>
                </div>
            </div>
        </div>
        <div class="stat_dresseur">
            <div class="localisation">
                Votre localisation : {{this.data.localisation[this.data.actual_localisation].name}}
            </div>
            <div class="nom">
                <div>Votre nom : {{data.trainer.name_trainer }}</div><br>
            </div>
            <div class="bag">
                <div>Montant pokedollar : {{this.data.trainer.pokedollar}}</div>
                <button @click="displayBag">Voir le contenu du sac</button>
                <div v-if="bag">
                    <!-- v-for="(pokemon, i) in team" :key="i" -->
                        <div v-for="(p,i) in this.data.trainer.bag" :key="i">
                            <button @click="useProuct(p,i)">{{p.name}}</button>
                        </div>
                </div>
            </div>
            <div class="hungry">
                    <div class="barre_exp">
                        <div class="stat_hungry" :style="{ width: data.trainer.stat_hungry * 2+ 'px' }">

                        </div>
                    </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'List', 
    data : function() {
      return {
        bag: false,
      }
    },
    props : {data : Object,
    team : Array,
    pkmn : Array},
    methods : {
        displayStat: function () {
            // console.log(this.pkmn[0].ability)
        },
         atk : function (a) {
          this.$emit("attack",a);
        },
        displayBag : function() {
            this.bag ? this.bag = false : this.bag = true
        },
        useProuct : function (p,i) {
            console.log(i)
            switch (p.effect) {
                case 'eat':
                    this.data.trainer.stat_hungry = 100;
                    this.data.trainer.bag.splice(i,1);
                break;
                case 'pokeball' :
                break;
                case 'potion' :
                break;
            }

        }
    },
    beforeMount(){
        // this.displayStat();
    },
}
</script>

<style>
/* 
    ================================
        Best Viewed In Full Page
    ================================
*/


#List {
    border: 1px solid black;
    border-radius:100px;
}
.stat {
    display: flex;
    flex-direction: column;
    align-items: center;
}
.thumbnail-pkmn {
    display:flex;
    border:1px solid black;
    max-width:50%;
}
.entry {
    width: 100%; 
    /* display:flex;
    justify-content: space-evenly; */
}
.mini_barre_exp {
    width:100px;
    height:24px;
    border :1px solid black;
}
.barre_exp {
    animation: 3s linear 1s slidein;
    width:200px;
    height:24px;
    border :1px solid black;
}
.stat_dresseur {
    display: flex;
    flex-direction: column;
    align-items: center;
}
.stat_hp {
    height:100%;
    /* width: 0px; */
    background-color:red;
}
.stat_exp {
    height:100%;
    background-color:blue;
}
.stat_hungry {
    height:100%;
    background-color:green;
}


/* Hover over a card to flip, can tab too. */

@import url('https://fonts.googleapis.com/css?family=Lato');
*,
*::after,
*::before {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
/* .flip-card-container */
.flip-card-container {
  --hue: 150;
  --primary: hsl(var(--hue), 50%, 50%);
  --white-1: hsl(0, 0%, 90%);
  --white-2: hsl(0, 0%, 80%);
  --dark: hsl(var(--hue), 25%, 10%);
  --grey: hsl(0, 0%, 50%);

  width: 310px;
  height: 500px;
  margin: 40px;

  perspective: 1000px;
}

/* .flip-card */
.flip-card {
  width: inherit;
  height: inherit;

  position: relative;
  transform-style: preserve-3d;
  transition: .6s .1s;
}

/* hover and focus-within states */
.flip-card-container:hover .flip-card,
.flip-card-container:focus-within .flip-card {
  transform: rotateY(180deg);
}

/* .card-... */
.card-front,
.card-back {
  width: 100%;
  height: 100%;
  border-radius: 24px;

  background: var(--dark);
  position: absolute;
  top: 0;
  left: 0;
  overflow: hidden;

  backface-visibility: hidden;

  display: flex;
  justify-content: center;
  align-items: center;
}

/* .card-front */
.card-front {
  transform: rotateY(0deg);
  z-index: 2;
}

/* .card-back */
.card-back {
  transform: rotateY(180deg);
  z-index: 1;
}

/* figure */
figure {
  z-index: -1;
}

/* figure, .img-bg */
figure,
.img-bg {
  position: absolute;
  top: 0;
  left: 0;

  width: 100%;
  height: 100%;
}

/* img */
img {
  height: 100%;
  border-radius: 24px;
}

/* figcaption */
figcaption {
  display: block;

  width: auto;
  margin-top: 12%;
  padding: 8px 22px;

  font-weight: bold;
  line-height: 1.6;
  letter-spacing: 2px;
  word-spacing: 6px;
  text-align: right;

  position: absolute;
  top: 0;
  right: 12px;

  color: var(--white-1);
  background: hsla(var(--hue), 25%, 10%, .5);
}

/* .img-bg */
.img-bg {
  background: hsla(var(--hue), 25%, 10%, .5);
}

.card-front .img-bg {
  clip-path: polygon(0 20%, 100% 40%, 100% 100%, 0 100%);
}

.card-front .img-bg::before {
  content: "";

  position: absolute;
  top: 34%;
  left: 50%;
  transform: translate(-50%, -50%) rotate(18deg);

  width: 100%;
  height: 6px;
  border: 1px solid var(--primary);
  border-left-color: transparent;
  border-right-color: transparent;

  transition: .1s;
}

.card-back .img-bg {
  clip-path: polygon(0 0, 100% 0, 100% 80%, 0 60%);
}

/* hover state */
.flip-card-container:hover .card-front .img-bg::before {
  width: 6px;
  border-left-color: var(--primary);
  border-right-color: var(--primary);
}

/* ul */
ul {
  padding-top: 50%;
  margin: 0 auto;
  width: 70%;
  height: 100%;

  list-style: none;
  color: var(--white-1);

  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

/* li */
li {
  width: 100%;
  margin-top: 12px;
  padding-bottom: 12px;

  font-size: 14px;
  text-align: center;

  position: relative;
}

li:nth-child(2n) {
  color: var(--white-2);
}

li:not(:last-child)::after {
  content: "";

  position: absolute;
  bottom: 0;
  left: 0;

  width: 100%;
  height: 1px;

  background: currentColor;
  opacity: .2;
}

/* button */
button {
  font-family: inherit;
  font-weight: bold;
  color: var(--white-1);

  letter-spacing: 2px;

  padding: 9px 20px;
  border: 1px solid var(--grey);
  border-radius: 1000px;
  background: transparent;
  transition: .3s;

  cursor: pointer;
}

button:hover,
button:focus {
  color: var(--primary);
  background: hsla(var(--hue), 25%, 10%, .2);
  border-color: currentColor;
}

button:active {
  transform: translate(2px);
}

/* .design-container */
.design-container {
  --tr: 90;
  --op: .5;

  width: 100%;
  height: 100%;

  background: transparent;
  position: absolute;
  top: 0;
  left: 0;

  pointer-events: none;
}

/* .design */
.design {
  display: block;

  background: var(--grey);
  position: absolute;

  opacity: var(--op);
  transition: .3s;
}

.design--1,
.design--2,
.design--3,
.design--4 {
  width: 1px;
  height: 100%;
}

.design--1,
.design--2 {
  top: 0;
  transform: translateY(calc((var(--tr) - (var(--tr) * 2)) * 1%))
}

.design--1 {
  left: 20%;
}

.design--2 {
  left: 80%;
}

.design--3,
.design--4 {
  bottom: 0;
  transform: translateY(calc((var(--tr) + (var(--tr) - var(--tr))) * 1%))
}

.design--3 {
  left: 24%;
}

.design--4 {
  left: 76%;
}

.design--5,
.design--6,
.design--7,
.design--8 {
  width: 100%;
  height: 1px;
}

.design--5,
.design--6 {
  left: 0;
  transform: translateX(calc((var(--tr) - (var(--tr) * 2)) * 1%));
}

.design--5 {
  top: 41%;
}

.design--6 {
  top: 59%;
}

.design--7,
.design--8 {
  right: 0;
  transform: translateX(calc((var(--tr) + (var(--tr) - var(--tr))) * 1%))
}

.design--7 {
  top: 44%;
}

.design--8 {
  top: 56%;
}

/* states */
button:hover+.design-container,
button:active+.design-container,
button:focus+.design-container {
  --tr: 20;
  --op: .7;
}

.abs-site-link {
  position: fixed;
  bottom: 20px;
  left: 20px;
  color: hsla(0, 0%, 100%, .6);
  font-size: 16px;
  font-family: 'Segoe UI', -apple-system, BlinkMacSystemFont, sans-serif;
}
</style>