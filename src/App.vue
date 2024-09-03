  <template>
   
    <main class="flex justify-center items-start w-full h-[97.7vh] p-12">
     
    <div class="w-[1000px]">
      <header class="flex justify-between items-center border-b-2 pb-2 border-blue-300">
        <h1 class="text-4xl">Notes</h1>
        <button class="p-2 bg-blue-700 rounded-full text-center text-white h-12 w-12 text-2xl font-bold" @click="toggleModal">+</button>
      </header>
<div class="flex flex-row justify-normal gap-2 flex-wrap mt-6 p-2" >
    <div class="w-44 h-52 rounded-md flex flex-col justify-between p-6" v-for="note in notes" :key="note.id" :style="{background:note.backgroundColor}">
    <h1 class="text-base">{{note.text}}</h1>
    <p class="font-semibold text-sm">{{ note.date }}</p>
    </div>
</div>
    </div>
    <div class="flex justify-center items-center w-full h-screen p-12 absolute z-10 top-0 bg-black/65" v-if="showModal">
     <div class="bg-white p-6 rounded-md min-w-fit shadow-sm shadow-white/45">
      <h1 class="font-semibold text-xl">New Task</h1>
      <textarea name="text" id="" cols="30" rows="7" class="border-2 border-blue-300 my-4 p-2 rounded-md  text-lg" v-model="newNote"></textarea>
      <div class="flex justify-end items-center gap-4">
        <button class="bg-red-600 text-white p-3 rounded-md w-24 hover:ring-2 ring-offset-2 ring-red-700" @click="closeModal">CANCEL</button>
        <button class="bg-blue-600 text-white p-3  rounded-md w-24 hover:ring-2 ring-offset-2 ring-blue-700" @click="createTask">CREATE</button>
      </div>
     </div>
   </div>
    </main>
  

  </template>

  <script setup>
import {ref} from "vue";
const newNote = ref("");
const showModal = ref(false);
const notes = ref([]);

const toggleModal =()=>{
  showModal.value = true;
}
const closeModal =()=>{
  showModal.value = false;
  newNote.value ="";
}

const getRandomColors =()=>{
  return "hsl( " + Math.random() * 360 + " 100%,75%) ";
}

const date = new Date();
const dateTime = "Craeted on : " +date.getDate() + "/"
                + (date.getMonth()+1)  + "/" 
                + date.getFullYear() + " At "  
                + date.getHours() + ":"  
                + date.getMinutes() + ":" 
                + date.getSeconds();

const createTask =()=>{
  if(newNote.value.length >1){
    showModal.value = false;
    notes.value.push({
  id : Math.floor(Math.random() * (1000 - 0.5 + 1) + 0.5 ),
  text: newNote.value,
  date: dateTime,
  backgroundColor : getRandomColors()
 });
 console.log(notes.value);
 newNote.value ="";
  }

}

  </script>

  <style scoped>
    @tailwind base;
    @tailwind components;
    @tailwind utilities;

    *{
      margin:0;
      padding: 0;
      box-sizing: border-box;
    }


  </style>