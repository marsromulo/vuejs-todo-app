<template>
    <div class="mb-3 mt-3">
        <form @submit="onSubmit">
        <div class="form-group w-100">
            <input type="text"  v-model="title"  class="form-control"  placeholder="Enter todo">
        </div>
        <button type="submit" :class="[titleToEdit === '' ? 'btn-success':'btn-warning', 'btn']">
            <span v-if="titleToEdit === ''">
                Add
            </span>
            <span v-else>
                Update
            </span>
            </button>
        </form>
    </div>
</template>

<script>

export default {
    name: "AddTodo",
    props: {
        titleToEdit:String,
        idToEdit:Number
    },
   data() {
    return {
        title:"",
        completed:false
    }
   },
    methods: {
       onSubmit(e){
        e.preventDefault();
        
        if(!this.title){
            alert('Please add title')
            return
        }

        if(!this.titleToEdit){
            const newTodo = {
                id:Math.floor(Math.random() * 100000000),
                title: this.title,
                completed:false
            }
            this.title ='';
            this.$emit('add-todo', newTodo);
        }else{
       
            this.$emit('update-todo', {id:this.idToEdit, title:this.title})   
        }
       }
    },

    watch: {
        titleToEdit:  function(newVal){
            this.title = newVal;
        }
    }
}
</script>
<style scoped>
    form {
        display: flex;
    }
    .btn {
        border-radius:0 !important;
        border-top-right-radius: 5px !important;
        border-bottom-right-radius: 5px !important;
    }

    input {
        border-top-right-radius: 0px !important;
        border-bottom-right-radius: 0px !important;
    }
</style>
