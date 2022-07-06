<template>
  <div class=" bg-gray-600 text-white w-1/2 m-auto mt-12">
    <div class="text-center border-b-2 border-black py-4">
       <h1 class="text-3xl py-4">ToDo-Liste</h1>
       <p class="text-xl" v-if="openTodos.length > 0">Offene ToDo's: {{ openTodos.length }}</p>
        <p class="text-xl" v-else>Momentan keine ToDos zu erledigen!</p>
       <div class="m-4">
        <input type="text" class="py-2 w-2/3 text-black" v-model="newTodo"/>
        <button class="bg-red-400 py-2 w-1/3" @click="addToDo">Add</button> 
       </div>
    </div>
    
    <div >
      <table>
    <tr>
      <th><b>Name &nbsp;</b></th>
      <th><b>Rating &nbsp;</b> </th>
      <th><b>Delete </b> </th>
    </tr>
    <tr v-for="(todo, index) in todos" :key="todo.name">
     <ToDoApp 
       :todosprob = "todos"
       :todoprop="todo" 
       :todoindex="index" 
       @toggledone-index="toggleDone(index)"
       @removetodo-index="removeToDo(index)"
       />
    </tr>
  
  </table>
      

    </div>
   <button @click="alertName()" >Sort by first name</button>
  </div>
 
</template>

<script>
import ToDoApp from './components/ToDoApp.vue'

export default {
  name: 'App',
  data() {
    return {
      newTodo: "",
      todos: [],
    }
  },  
  methods: {
    alertName: function(){
        this.todos.name.sort(); /** sort function is throwing an error here **/
      console.log(this.todos.name); /** and this does not format array objects followed by first name **/
    },
  toggleDone(index){
      this.todos[index].done = !this.todos[index].done;
      this.storeTodos();
    },
    removeToDo(index){
      this.todos.splice(index, 1); 
      this.storeTodos();
    },
    addToDo(){
      if(this.newTodo.trim() == ""){
        return;
      }
      this.todos.push({name: this.newTodo, done: false });
      this.storeTodos();
    },
    storeTodos(){
      localStorage.setItem("todos",JSON.stringify(this.todos))
    }
  },
  mounted(){
    let data = localStorage.getItem("todos");
    if(data !== "" && data !== null){
      this.todos = JSON.parse(data);
    } else {
      this.todos = [];
    }
  },
  components: {
    ToDoApp,
    
  },
  computed: {
    openTodos(){

      const openToDos = this.todos.filter((name) => {
        return !name.done
      });
      return openToDos;
    },
   
  },
};
</script>

