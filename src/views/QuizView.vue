<template>
  <div>
    <QuizHeader
      :questionStatus="questionStatus"
      :barPercentage="barPercentage"
    />
    <div>
      <Question
        v-if="showResults"
        @selectOption="optionSelected"
        :question="quiz.questions[currentQuestionIndex]"
      />
      <Result
        :questionLength="quiz.questions.length"
        :correctAnswers="noOfCorrectAnswers"
        v-else
      />
    </div>
    <button v-if="showResults" @click="currentQuestionIndex++">
      Next Question
    </button>
  </div>
</template>

<script setup>
import Question from "../components/Question.vue";
import QuizHeader from "../components/QuizHeader.vue";
import Result from "../components/Result.vue";
import { ref, computed } from "vue";
import { useRoute } from "vue-router";
import q from "../data/quizes.json";

const route = useRoute();

const quizId = parseInt(route.params.id);
const quiz = q.find((quiz) => quiz.id === quizId);
const currentQuestionIndex = ref(0);
const noOfCorrectAnswers = ref(0);
const showResults = ref(true);

// const questionStatus = ref(
//   `${currentQuestionIndex.value}/${quiz.questions.length}`
// );

// watch(
//   () => currentQuestionIndex.value,
//   () => {
//     questionStatus.value = `${currentQuestionIndex.value}/${quiz.questions.length}`;
//   }
// );

const questionStatus = computed(
  () => `${currentQuestionIndex.value} / ${quiz.questions.length}`
);

const barPercentage = computed(
  () => `${(currentQuestionIndex.value / quiz.questions.length) * 100}%`
);

const optionSelected = (isCorrect) => {
  if (isCorrect) {
    noOfCorrectAnswers.value++;
  }

  if (quiz.questions.length - 1 === currentQuestionIndex.value) {
    showResults.value = false;
  }
  currentQuestionIndex.value++;
};
</script>

<style scoped></style>
