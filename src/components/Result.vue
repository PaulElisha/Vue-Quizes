<template>
  <div class="results">
    <p>Your results...</p>
    <h1>{{ correctAnswers }}/{{ questionLength }}</h1>
    <RouterLink to="/">Go Home</RouterLink>
  </div>
</template>

<script setup>
import { defineProps } from "vue";
import { RouterLink } from "vue-router";

const { correctAnswers, questionLength } = defineProps([
  "correctAnswers",
  "questionLength",
]);
</script>

<style scoped>
.results {
  text-align: center;
  padding: 100px 0;
}

p {
  font-size: 25px;
}

h1 {
  font-size: 80px;
}
</style>
