<template>
  <AddTodo 
  @add-todo="addTodo"></AddTodo>
  <TodoItem v-for="todo in todos" 
  v-bind:key="todo.id" 
  v-bind:TodoProps="todo" 
  v-on:item-completed="markCompleted"
  @delete-item="deleteTodo"
  @edit-item="editTodo"
  > </TodoItem>
</template>

<script>
import { ref } from 'vue';
import TodoItem from "./TodoItem.vue"
import AddTodo from "./AddTodo.vue";
import axios from "axios"

export default {
    name:"TodosApp",
    components:{
        TodoItem,AddTodo
     },
    setup() {
        const todos = ref([])

        const getAllTodos = async () =>{
            try {
                const res = await axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5');
                todos.value = res.data;
            } catch (error) {
                console.log(error)
            }
        }
        getAllTodos()

        const markCompleted = function(id) {
            todos.value = todos.value.map(todo => {
                if(todo.id===id)
                todo.completed =!todo.completed;
                return todo
            })
        }

        const deleteTodo = async id => {
            try {
                await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
                todos.value = todos.value.filter(todo => todo.id !==id)
            } catch (error) {
                console.log(error)
            }
            
        }

        const addTodo = async newTodo=>{
            try {
                const res =await axios.post('https://jsonplaceholder.typicode.com/todos', newTodo)
                todos.value.push(res.data)
            } catch (error) {
                console.log(error)
            }
        }

        // const editTodo = function(){

        // }
        return {
            todos,
            markCompleted,
            deleteTodo,
            addTodo,
            
            // editTodo
        }
    }
}
</script>

<style>

</style>