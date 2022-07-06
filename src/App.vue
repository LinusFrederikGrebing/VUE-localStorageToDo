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
    <table class="w-full">
    <tr class="flex justify-between items-center py-2 px-2">
      <th><b @click="sortName()">Name &nbsp;</b></th>
      <th class="ml-auto px-20"><b @click="sortRating()">Rating &nbsp;</b> </th>
      <th><b>Delete </b> </th>
    </tr>
    <tr v-for="(todo, index) in todos" :key="todo.name">
     <ToDoApp 
       :todosprob = "todos"
       :todoprop="todo" 
       :todoindex="index" 
       @saveCount = "saveCount()"
       />
    </tr>
  
  </table>

    </div>
   <div class="text-center">VUE-Projekt</div>
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
      toggleRating: false,
      toggleName: false,
    }
  },  
  methods: {
    sortRating(){
      if(this.toggleRating == false) { this.todos.sort((a, b) => a.count < b.count ? 1 : -1); this.toggleRating = true;}
      else { this.todos.sort((a, b) => a.count > b.count ? 1 : -1); this.toggleRating = false;}
    },
    sortName(){
      if(this.toggleName == false) { this.todos.sort((a, b) => a.name.toUpperCase() < b.name.toUpperCase() ? 1 : -1); this.toggleName = true;}
      else { this.todos.sort((a, b) => a.name.toUpperCase() > b.name.toUpperCase() ? 1 : -1); this.toggleName = false; }
    },
    saveCount(){
         this.storeTodos();
    },
    addToDo(){
      if(this.newTodo.trim() == ""){
        return;
      }
      this.todos.push({name: this.newTodo, done: false, count: 0 });
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

