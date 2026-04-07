# Zadatak za vježbu: Vue Task Tracker

**Cilj:** Izraditi modularnu aplikaciju za upravljanje zadacima koja koristi hijerarhiju komponenti, dvosmjernu komunikaciju i fleksibilne slotove.

### Specifikacija:
1.  **`TaskCard.vue`**: Komponenta koja prikazuje jedan zadatak.
    * Prima `naslov` (string, obavezan) i `prioritet` (broj, default: 1) kao **props**.
    * Sadrži tipku "Završi" koja šalje **emit** događaj roditelju.
    * Koristi **slot** za opcionalni opis zadatka.
2.  **`TaskList.vue`**: Komponenta koja prima niz objekata (zadataka) i prikazuje ih koristeći `TaskCard`.
    * Implementira **validaciju props-a** za listu zadataka.
3.  **`App.vue`**: Glavna komponenta koja drži stanje (listu zadataka) i upravlja logikom brisanja.

---

# Rješenje zadatka

### 1. Komponenta `TaskCard.vue`
Ovdje pokrivamo: `defineProps` s validacijom, `defineEmits` i osnovni `<slot>`.

```html
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
```

### 2. Komponenta `TaskList.vue`
Ovdje pokrivamo: Prosljeđivanje props-a djetetu i prosljeđivanje emita prema gore.

```html
<script setup>
import TaskCard from './TaskCard.vue';

// Validacija da je 'tasks' niz (array)
defineProps({
  tasks: {
    type: Array,
    required: true
  }
});

const emit = defineEmits(['ukloniIzListe']);
</script>

<template>
  <div class="task-list">
    <TaskCard 
      v-for="(t, index) in tasks" 
      :key="index"
      :naslov="t.naslov"
      :prioritet="t.prioritet"
      @zavrsi-task="emit('ukloniIzListe', index)"
    >
      <p v-if="t.opis">{{ t.opis }}</p>
    </TaskCard>
  </div>
</template>
```

### 3. Glavna komponenta `App.vue`
Ovdje pokrivamo: Upravljanje stanjem, uvoz komponenti i reaktivnost.

```html
<script setup>
import { ref } from 'vue';
import TaskList from './components/TaskList.vue';

const mojiZadaci = ref([
  { naslov: 'Naučiti Vue komponente', opis: 'Proučiti props, emits i slotove.', prioritet: 3 },
  { naslov: 'Otići u teretanu', opis: '', prioritet: 1 },
  { naslov: 'Skuhati ručak', opis: 'Pasta Carbonara.', prioritet: 2 }
]);

function obrisiZadatak(index) {
  mojiZadaci.value.splice(index, 1);
  alert("Zadatak uspješno odrađen!");
}
</script>

<template>
  <div class="container">
    <h1>My Task Tracker</h1>
    <hr />
    <TaskList :tasks="mojiZadaci" @ukloni-iz-liste="obrisiZadatak" />
    
    <p v-if="mojiZadaci.length === 0">Čestitamo! Svi zadaci su obavljeni.</p>
  </div>
</template>

<style>
.container {
  max-width: 600px;
  margin: 0 auto;
  font-family: Arial, sans-serif;
  text-align: center;
}
</style>
```
---
