<script setup>
import { ref } from 'vue';

const emit = defineEmits(['dodaj']);

// Lokalno stanje za formu
const noviNaslov = ref('');
const noviOpis = ref('');
const noviPrioritet = ref(1);

function submitForme() {
  if (noviNaslov.value.trim() === '') return;

  // Emitiramo objekt s podacima
  emit('dodaj', {
    naslov: noviNaslov.value,
    opis: noviOpis.value,
    prioritet: noviPrioritet.value
  });

  // Resetiranje polja nakon dodavanja
  noviNaslov.value = '';
  noviOpis.value = '';
  noviPrioritet.value = 1;
}
</script>

<template>
  <div class="add-task-form">
    <input v-model="noviNaslov" placeholder="Naslov zadatka..." />
    <input v-model="noviOpis" placeholder="Opis (opcionalno)..." />
    <input v-model.number="noviPrioritet" type="number" min="1" max="5" />
    <button @click="submitForme">Dodaj zadatak</button>
  </div>
</template>

<style scoped>
.add-task-form {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-bottom: 20px;
  padding: 15px;
  background: #ee0909;
  border-radius: 5px;
}
</style>