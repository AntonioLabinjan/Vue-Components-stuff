<script setup>
import { ref } from 'vue';
import TaskList from './components/TaskList.vue';
import AddTask from './components/AddTask.vue';

const mojiZadaci = ref([
  { naslov: 'Naučiti Vue komponente', opis: 'Proučiti props, emits i slotove.', prioritet: 3 }
]);

// Metoda za dodavanje novog zadatka u niz (reaktivnost na djelu!)
function dodajNoviZadatak(zadatak) {
  mojiZadaci.value.push(zadatak);
}

function obrisiZadatak(index) {
  mojiZadaci.value.splice(index, 1);
}
</script>

<template>
  <div class="container">
    <h1>My Task Tracker</h1>
    <hr />
    
    <AddTask @dodaj="dodajNoviZadatak" />
    
    <TaskList :tasks="mojiZadaci" @ukloni-iz-liste="obrisiZadatak" />
    
    <p v-if="mojiZadaci.length === 0">Sve je obavljeno!</p>
  </div>
</template>
<style>
.container {
  max-width: 600px;
  margin: 0 auto;
  font-family: Arial, sans-serif;
  text-align: center;
  color: aquamarine;
}
</style>