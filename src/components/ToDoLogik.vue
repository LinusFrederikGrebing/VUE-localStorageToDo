<template>
  <div class="flex justify-between items-center py-2 px-2 text-black bg-slate-200">

    <h1 class="cursor-pointer block text-base" :class="{'line-through': this.myToDo.done, 'no-underline ': !this.myToDo.done}" @click="toggleTodo" >{{ myToDo.name }}</h1>
    
    <div class="flex items-center ml-auto px-6 ">
        <h1 class="mx-3">{{ myToDo.count }} / 5</h1>
        <button class="bg-black p-2 " v-if="myToDo.count < 5" @click="countUp"><div class="h-0 w-0 border-x-8 border-x-transparent border-b-[16px] border-b-white-600"></div></button>
        <button class="bg-black p-2 " v-else><div class="h-0 w-0 border-x-8 border-b-[16px] border-b-white-600 border-opacity-5"></div></button>
        <button class="bg-black p-2  mx-1" v-if="myToDo.count > 0"  @click="countDown"><div class="h-0 w-0 border-x-8 border-x-transparent border-t-[16px] border-b-white-600"></div></button>
        <button class="bg-black p-2  mx-1" v-else><div class="h-0 w-0 border-x-8  border-t-[16px]"></div> </button>
     </div>
     <button class="bg-red-700 py-1 ml-10 mr-1 px-4 text-white" @click="removeToDo">X</button>
  </div>
</template>

<script>
export default {
  name: 'ToDoLogik',
  props: ["todoprop", "todoindex", "todosprob"],
  data(){
    return {
      myToDo: this.todoprop,
      myToDoArray: this.todosprob

    };
  },
  methods: {

    countUp(){
        this.myToDo.count++; 
        this.$emit("saveCount");
      },

    countDown(){
      this.myToDo.count--;
      this.$emit("saveCount");
    },
  
    toggleTodo(){
      this.myToDoArray[this.todoindex].done = !this.myToDoArray[this.todoindex].done;
      this.$emit("saveCount");
    },
    removeToDo() {
       this.myToDoArray.splice(this.todoindex, 1); 
       this.$emit("saveCount");
    }
  },
  computed: {
   
  }
};
</script>


