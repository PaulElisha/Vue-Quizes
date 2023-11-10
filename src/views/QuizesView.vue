<template>
  <div>
    <header>
      <h1>Quizes</h1>
      <input type="text" v-model="search" placeholder="search..." />
    </header>
    <div class="options-container">
      <Card v-for="quiz in quizes" :key="quiz.id" :quiz="quiz" />
    </div>
  </div>
</template>

<script setup>
import q from "../data/quizes.json";
import Card from "../components/Card.vue";
import { ref, watch } from "vue";

const quizes = ref(q);
const search = ref("");

watch(search, () => {
  quizes.value = q.filter((quiz) =>
    quiz.name.toLowerCase().includes(search.value)
  );
});
</script>

<style scoped></style>
