<script setup>
// Definiranje props-a s validacijom
const props = defineProps({
  naslov: {
    type: String,
    required: true
  },
  prioritet: {
    type: Number,
    default: 1
  }
});

// Definiranje emita
const emit = defineEmits(['zavrsiTask']);

function oznaciKaoZavrseno() {
  emit('zavrsiTask');
}
</script>

<template>
  <div class="task-card">
    <h3>{{ naslov }} (Prioritet: {{ prioritet }})</h3>
    
    <div class="opis-slota">
      <slot><i>Nema opisa za ovaj zadatak.</i></slot>
    </div>

    <button @click="oznaciKaoZavrseno">Završi zadatak</button>
  </div>
</template>

<style scoped>
.task-card {
  border: 1px solid #ccc;
  padding: 1rem;
  margin: 1rem 0;
  border-radius: 8px;
  background-color: #f9f9f9;
}
button {
  background-color: #42b883;
  color: white;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
}
</style>