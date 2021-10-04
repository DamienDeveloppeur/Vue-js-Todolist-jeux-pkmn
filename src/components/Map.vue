<template>
    <div id="map">
        <div class="pad">
            <!-- <div class="arrow top" ></div> -->
            <button v-on:click="moove(true)">Aller en haut</button>
            <button v-on:click="moove(false)">Aller en bas</button>
            <!-- <div class="arrow right"></div> -->
            <!-- <div class="arrow bottom" v-on:click="moove(false)"></div> -->
            <!-- <div class="arrow left"></div> -->
        </div>
    </div>
</template>

<script>
export default {
    name: 'Map', 
    props : {data : Object,
    team : Array},
    methods : {
        moove (moove) {
            // this.data.localisation.indexOf(this.data.localisation[this.data.actual_localisation + 1]) > -1 ? console.log("yes") : console.log("no");
            if(moove && this.data.localisation.indexOf(this.data.localisation[this.data.actual_localisation + 1]) > -1)this.data.actual_localisation++;
            else if (!moove && this.data.localisation.indexOf(this.data.localisation[this.data.actual_localisation - 1]) > -1) this.data.actual_localisation--;
        }
    }
}
</script>

<style>
#map {
    /* min-height: 500px; */
}
.arrow:before {
    /* position: relative; */
    content: "";
    display: inline-block;
    width: 0.4em;
    height: 0.4em;
    border-right: 0.2em solid black;
    border-top: 0.2em solid black;
    margin-right: 0.5em;
    font-size:50px;
}
.right {
    transform: rotate(45deg);
    position:relative;
    top:11%;
    left:3%;
}
.left {
    transform: rotate(225deg);
    position: relative;
    left: -7%;
    bottom: 52%;
}
.bottom {
    transform: rotate(-225deg);
    position: relative;
    left: -2%;
    bottom:-101%;
}
.top {
    transform: rotate(-45deg);
}
</style>