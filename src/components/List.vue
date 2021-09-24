<template>
   <ul id="List">
        <li v-for="(item, i) in items" :key="item.id">
          {{ item.element }} 
          <span @click="del_func(i)">Delete</span>
          <span v-bind:style="{background : (item.done ? 'green' : 'red')}" @click="acomplished(i)">Noter comme acompli</span>
        </li>
    </ul>
</template>

<script>
export default {
    name: 'List', 
    props : {items : Array},
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