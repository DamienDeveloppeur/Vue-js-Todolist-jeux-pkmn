<template>
    <ul id="List">
        <li>
          {{ data.name_pkmn }} 
        </li>
    </ul>
</template>

<script>
export default {
    name: 'List', 
    props : {data : Array},
    methods : {
        del_func: function (index) {
            this.items.splice(index, 1);
        },
        acomplished: function (index) {
            this.items[index].done = true;
        }
    }
}
</script>

<style>

</style>