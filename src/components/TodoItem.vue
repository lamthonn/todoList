<template>
    <p :class="['todoItem', {'is-completed' :TodoProps.completed}]" >
        <input type="checkbox" :checked="TodoProps.completed" v-on:change="markItemCompleted">
        {{ TodoProps.title }}
        
        <button class="del-btn" @click="deleteItem">Delete</button>
        <button class="edit-btn" @click="editItem">Edit</button>
        
    </p>
</template>

<script>
// import { ref } from 'vue';

export default {
    name:'TodoItem',
    props: ['TodoProps'],
    setup(props, context) {
        // const editedTask=ref(null)

        // const statuses= ["to-do","in-progress","finished"]

        const markItemCompleted = () =>{
            context.emit('item-completed', props.TodoProps.id);
        }

        const deleteItem= function() {
            context.emit('delete-item', props.TodoProps.id);
        }

        // const editItem= function(){
        //     context.emit('edit-item', props.TodoProps.id);
        // }
    return {
        // editedTask,
        // statuses,
        markItemCompleted,
        deleteItem,
        // editItem
    }
    } 
    
}
</script>

<style scope>
.del-btn{
    background: red;
    color: #fff;
    cursor: pointer;
    float: right;
    border: none;
}
.del-btn:hover{
    background: rgb(141, 2, 2);
    scale: 1.1;
}

.edit-btn{
    background: greenyellow;
    color: #fff;
    cursor: pointer;
    float: right;
    border: none;
    margin-right: 10px;
}
.edit-btn:hover{
    background: rgb(77, 125, 4);
    scale: 1.1;
}

.todoItem{
    background: #f4f4f4;
    padding:10px ;
    margin: 0;
    border-bottom: 1px #ccc dotted;
}

.is-completed{
    text-decoration: line-through;
}
</style>