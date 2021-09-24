<template>
    <form id="Form" @submit="onSubmitForm">
        <p>
            <label for="name">Element à ajouter</label>
            <input v-model="name" type="text">
        </p>
        <p>
            <input type="submit" value="Submit">
        </p>
    </form>
</template>

<script>
export default {
    name: "Form",
    data : function() {
      return {
        name: null,
      }
    },
    props : {items : Array},
    methods:{
        onSubmitForm: function() {
            const task = {
                title: this.title,
                content: this.content
            };
            this.$emit('addTask',task);
        },
        
      checkForm: function (e) {
        console.log(this.items)
        //console.log(element_todo.items.length)
        this.items.push({element: this.name, done: false});
        e.preventDefault();
      }
    }
}
</script>

<style>

</style>