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