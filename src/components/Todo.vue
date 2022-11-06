<template>
    <li 
        :class="[todo.completed ? 'completed':'', 'task']" 
        @dblclick="$emit('toggle-completed', todo.id)"
    >
        <span>{{ todo.title }} </span>
        
        <span>
            <i class="fa-regular fa-pen-to-square" style="cursor:pointer; margin-right:20px;"
                @click="$emit('edit-todo', todo)"
            ></i>
            <i class="fa-solid fa-xmark" 
                @click="$emit('delete-todo', todo.id)" 
            ></i>
        </span>
    </li>
    
</template>

<script>

export default {
    name: "Todo",
    props: ['todo'],
    emits: ['delete-todo', 'toggle-completed', 'edit-todo']

}

</script>
<style scope>
.task {
    padding: 10px;
    background: #f4f4f4;
    margin-bottom: 1px;
    border-left:5px  solid green;
    display: flex;
    justify-content: space-between;
    cursor:pointer;
}
.fa-xmark{
    color:red;
}

.completed {
  border-left:5px  solid #d9d7d7;  
  text-decoration: line-through;
  color:#d9d7d7;
}

</style>
