<template>
  <div class="app">
    <header>
      <h1>Vue Note App</h1>
      <button @click="showModal = true">+</button>
    </header>
    <section class="card-container">
      <div
        v-for="el in notes"
        :key="el.id"
        :style="{ backgroundColor: el.color }"
        class="card"
      >
        <p class="main-text">{{ el.text }}</p>
        <p class="date">{{ el.date.toLocaleDateString() }}</p>
      </div>
    </section>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <textarea v-model="newNote" />
        <button class="btnl" @click="addNote">Add Note</button>
        <button @click="showModal = false">Close</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const newNote = ref("");
const notes = ref([]);
const showModal = ref(false);

const getRandomColor = () => {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
};

const addNote = () => {
  notes.value.push({
    id: Math.floor(Math.random() * 100000),
    text: newNote.value,
    color: getRandomColor(),
    date: new Date(),
  });
  showModal.value = false;
  newNote.value = "";
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
}

.app {
  max-width: 1300px;
  padding: 20px;
  margin: 0 auto;
}

header {
  display: flex;
  justify-content: space-between;
  margin: 40px auto;
  font-size: 20px;
}

header button {
  outline: none;
  border: none;
  width: 50px;
  height: 50px;
  background-color: black;
  border-radius: 50%;
  color: white;
  cursor: pointer;
  box-shadow: 3px 4px 53px -14px rgba(78, 61, 61, 0.64);
}
.card-container {
  display: flex;
  flex-wrap: wrap;
}
.card {
  width: 225px;
  height: 225px;
  background-color: rgb(237, 182, 44);
  padding: 10px;
  border-radius: 4px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 20px;
  margin-bottom: 20px;
  box-shadow: 3px 4px 53px -14px rgba(78, 61, 61, 0.185);
}
.main-text {
  line-height: 1.25;
  font-size: 17.5px;
  font-weight: bold;
}
.date {
  font-size: 12.5px;
  margin-top: auto;
}
.overlay {
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  position: absolute;
  background-color: rgba(128, 128, 128, 0.459);
  display: flex;
  justify-content: center;
  align-items: center;
  transition: ease 2s;
}

.modal {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
  position: relative;
  width: 700px;
  height: 350px;
  background-color: white;
  padding: 20px;
}

.modal textarea {
  width: 100%;
  height: 200px;
  font-size: 20px;
  outline: none;
  border-radius: 4px;
  padding: 20px;
}

.modal .btnl {
  background-color: rgb(15, 15, 83);
}

.modal button {
  width: 100%;
  padding: 15px;
  color: white;
  font-size: 20px;
  outline: none;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  background-color: brown;
}
</style>
