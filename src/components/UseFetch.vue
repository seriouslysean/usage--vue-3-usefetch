<script setup>
import { onMounted, ref } from 'vue';

const pokemon = ref([]);
const count = ref(0);

// Get data in mounted hook
onMounted(async () => {
  const response = await fetch(
    'https://pokeapi.co/api/v2/pokemon?limit=5&offset=0'
  );
  const json = await response.json();
  const results = json?.results || [];
  // Update refs
  pokemon.value = results;
  count.value = results.length;
});
</script>

<template>
  <div class="c-use-fetch">
    <h2>Count: {{ count }}</h2>
    <ol v-if="count > 0">
      <li v-for="{ name, url } in pokemon" :key="url">
        <a :href="url" :title="name">{{ name }}</a>
      </li>
    </ol>
  </div>
</template>
