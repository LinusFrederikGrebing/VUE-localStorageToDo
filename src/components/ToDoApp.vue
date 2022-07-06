<template>
  <div class="flex justify-between items-center py-2 px-2" :class="{'bg-green-600': this.myToDo.done, 'bg-red-600': !this.myToDo.done}">

     <table>
    <tr>
      <th><b>Name &nbsp;</b></th>
      <th><b>Rating &nbsp;</b> </th>
      <th><b>Delete </b> </th>
    </tr>
    <tr v-for="myToDo in myToDoArray" :key="myToDo.name">
      <td>{{ myToDo.name }}</td>
      <td>{{ count }}</td>
      <td> <button class="bg-black py-1 px-1 rounded" @click="removeToDo">Delete ToDo</button></td>
    </tr>
  
  </table>
    <!--<h1 class="cursor-pointer" @click="toggleTodo" >{{ myToDo.name }}</h1>
    
    <div class="flex items-center ml-auto px-6 ">
        <h1 class="mx-3">{{ count }} / 5</h1>
        <button class="bg-black p-2 rounded" v-if="count < 5" @click="countUp"><div class="h-0 w-0 border-x-8 border-x-transparent border-b-[16px] border-b-white-600"></div></button>
        <button class="bg-black p-2 rounded" v-else><div class="h-0 w-0 border-x-8 border-b-[16px] border-b-white-600 border-opacity-5"></div></button>
        <button class="bg-black p-2 rounded mx-1" v-if="count > 0"  @click="countDown"><div class="h-0 w-0 border-x-8 border-x-transparent border-t-[16px] border-b-white-600"></div></button>
        <button class="bg-black p-2 rounded mx-1" v-else><div class="h-0 w-0 border-x-8  border-t-[16px]"></div> </button>
     </div>
    
  -->
  </div>
</template>

<script>
export default {
  name: 'ToDoApp',
  props: ["todoprop", "todoindex", "todosprob"],
 /* data: function(){
    return{
      message: "Hello World",
      count: 0,
    };
  },
  */
  data(){
    return {
      count: 0,
      myToDo: this.todoprop,
      myToDoArray: this.todosprob

    };
  },
  methods: {
    
    countUp(){
        this.count++; 
      },

    countDown(){
      this.count--;
    },
  
    toggleTodo(){
      this.$emit("toggledone-index");
    },
    removeToDo() {
      this.$emit("removetodo-index");
    }
  },
  computed: {
   
  }
};
</script>


