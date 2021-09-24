<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <Form @addTask="onAddtask"/>
    <!-- v-bind:items="items"  -->
    <List v-bind:items="items" />
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import Form from './components/Form.vue'
import List from './components/List.vue'

export default {
  name: 'App',
  data : function() {
    return {
        items: [
            {element: 'Vuejs', done: false, id:1},
            {element: 'React', done: true, id:2}
        ],
      }
  },
  methods : {
    onAddTask : function (task) {
      this.items.push(task);
    }
  },
  components: {
    Form,
    List
  }
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
</style>
