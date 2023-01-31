<script setup>
  import { ref } from 'vue';

  const showModal = ref(false)
  const newNote = ref("")
  const errorMessage = ref("")
  const notes = ref([])
  const getRandomColor = ()=>{
    return 'hsla(' + (Math.random() * 360) + ', 100%, 50%, 1)'
  }
  const addNote = () =>{
    if (newNote.value.length === 0) {
      return errorMessage.value = "поле не может быть пустым!"
    }
    notes.value.push({
      id: Math.floor(Math.random()*10000),
      text: newNote.value,
      date: new Date().toLocaleDateString(),
      backgroundColor: getRandomColor()
    }),
    showModal.value = false,
    errorMessage.value = "",
    newNote.value = ""
    
  }
</script>

<template>
  <main>
    <div class="owerlay" v-if="showModal">
      <div class="modal">
        <h1 style="color: red;">{{ errorMessage }}</h1>
        <textarea v-model.trim="newNote"></textarea>
        <button class="add" @click="addNote()" >Add Node</button>
        <button class="close" @click="showModal = false">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal = true">+</button>
      </header>
      <div class="card-container">
        <div 
        class="card" 
        v-for="note in notes" 
        :style="{backgroundColor: note.backgroundColor}"
        :key="note.id"
        >
          <p class="main-text">{{ note.text }}</p>
          <p class="date">{{ note.date }}</p>
        </div>
      </div>
    </div>
  </main>
</template>


<style scoped>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
main{
  height: 100vh;
  width: 100vw;
}
.container{
  max-width: 1000px;
  padding: 10px;
  margin: 0 auto;
}
header{
  display: flex;
  justify-content: space-between;
  align-items: center;
}
h1{
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 45px;
}
header button{
  border: none;
  padding: 10px;
  width: 50px;
  height: 50px;
  cursor: pointer;
  background: black;
  border-radius: 50%;
  color: white;
  font-size: 20px;
}
.card-container{
  display: flex;
  flex-wrap: wrap;
}
.card{
  width: 225px;
  height: 225px;
  background-color: rgb(237, 182, 44);
  padding: 10px;
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin: 10px;
  font-size: 30px;
}
.date{
  font-size: 20px;
}
.owerlay{ 
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: black;
  opacity: 0.9;
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: .3s;
}
.modal{
  width: 750px;
  background-color: white;
  border-radius: 10px;
  padding: 30px;
  position: relative;
  display: flex;
  flex-direction: column;
}
.modal textarea{
  height: 350px;
  padding: 10px;  
  font-size: 20px;
}
.modal .add{
  margin-top: 15px;
  padding: 10px;
  background-color: plum;
  color: white;
  font-size: 15px;
  cursor: pointer;
  border: none;
  outline: none;
  transition: .3s;
}
.modal .add:hover{
  background-color: rgb(223, 185, 223);
  transition: .3s;
}
.modal .close{
  margin-top: 15px;
  padding: 10px;
  background-color: red;
  color: white;
  font-size: 15px;
  cursor: pointer;
  border: none;
  outline: none;
  transition: .3s;
}
.modal .close:hover{
  background-color: grey;
  transition: .3s;
}
</style>