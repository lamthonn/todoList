<template>
  <div id="app">
    <MytodoHeader></MytodoHeader>
    <TodosApp></TodosApp>
    
  </div>
</template>

<script>
import MytodoHeader from "./components/TodoHeader.vue";
import TodosApp from "./components/Mytodo.vue"


export default {
  name:"App",
  components:{
    MytodoHeader,
    TodosApp,
    
  }, 
}
</script>

<style>
 #app{
  font-family: Arial, Helvetica, sans-serif;
 }
</style>