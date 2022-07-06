<template>
  <div class="flex flex-col">
    <button class="w-2/12 bg-blue-500 hover:bg-blue-400 text-white font-bold py-2 px-4 border-b-4 border-blue-700 hover:border-blue-500 rounded" @click="renderToDoApp()"> ToDoApp </button>
    <button class=" w-2/12 bg-blue-500 hover:bg-blue-400 text-white font-bold py-2 px-4 border-b-4 border-blue-700 hover:border-blue-500 rounded" @click="renderInfoText()"> InfoText </button>
      <div v-if="this.todoapplication == true" >  <ToDoApp /> </div>
       <div v-if="this.infoapplication == true" >  <infoText /> </div>
    
    
  </div>
</template>

<script>
import ToDoApp from './components/ToDoApp.vue'
import infoText from './components/infoText.vue'

export default {
   name: 'App',
   data(){
    return {
      todoapplication: 0,
      infoapplication: 0,

    };
   },
   components: {
    ToDoApp,
    infoText,
},

   methods: {
    renderToDoApp(){
      if(this.todoapplication == false){ this.todoapplication = true; }
      else { this.closeToDoApp(); }
      this.closeInfoText();
    },
    
    closeToDoApp(){
      this.todoapplication = false;
    },

    renderInfoText(){
      if(this.infoapplication == false){ this.infoapplication = true; }
      else { this.closeInfoText();  }
       this.closeToDoApp();
    },

    closeInfoText(){
      this.infoapplication = false;
    },

   },
};
</script>

