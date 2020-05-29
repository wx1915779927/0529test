<template>
  <div class="todo-container">
    <div class="todo-wrap">
      <Header :addTodo="addTodo" />
      <Main :todos="todos" :deleteOne="deleteOne" :updateOne="updateOne" />
      <Footer :todos="todos" :updateAll="updateAll" :deleteAll="deleteAll" />
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
import Header from "./compones_test/Header.vue"
import Main from "./compones_test/Main.vue"
import Footer from "./compones_test/Footer.vue"
export default {
  components:{
    Header,
    Main,
    Footer
  },
  data(){
    return{
        todos:JSON.parse(localStorage.getItem('todos_key')) || []
      }
  },
   methods: {
    addTodo(obj){
      this.todos.unshift(obj)
    },
    deleteOne(index){
      this.todos.splice(index,1)
    },
    updateOne(index,val){
      this.todos[index].isOver = val
    },
    updateAll(val){
      this.todos.forEach(item => item.isOver = val)
    },
    deleteAll(){
      this.todos = this.todos.filter(item=>!item.isOver)
    }
  },
   watch:{
      // todos(newVal,oldVal){

      //       localStorage.setItem('todos_key',JSON.stringify(newVal))
      //   }
        todos:{
            deep:true,
            handler(newVal,oldVal){
                localStorage.setItem('todos_key',JSON.stringify(newVal))
            }
        }
    },
};
</script>

<style scoped>
.todo-container {
  width: 600px;
  margin: 0 auto;
}
.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
</style>
