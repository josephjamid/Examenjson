<script setup>
import { ref } from 'vue';


const questions = ref([
  {
    question: "Una palanca sirve para",
    options: [
      { text: "cortarse las uñas", correct: false },
      { text: "vencer una resistencia con poco esfuerzo", correct: true },
      { text: "saltar la comba", correct: false },
      { text: "apretar un tornillo", correct: false }
    ]
  },
  {  
    question: "¿Qué hace la fotosíntesis en las plantas?",
    options: [
      { text: "Transforma la luz solar en energía química", correct: true },
      { text: "Produce dióxido de carbono", correct: false },
      { text: "Consume agua y oxígeno", correct: false },
      { text: "Genera calor", correct: false }
    ]
  },
  {
    question: "¿Cuál es la capital de Francia?",
    options: [
      { text: "Madrid", correct: false },
      { text: "Berlín", correct: false },
      { text: "París", correct: true },
      { text: "Londres", correct: false }
    ]
  }
]);

const currentQuestionIndex = ref(0);
const answerStatus = ref(null);
const correctAnswers = ref(0);
const wrongAnswers = ref(0);

const buttonClasses = [
  'bg-red-500 hover:bg-red-700',
  'bg-blue-500 hover:bg-blue-700',
  'bg-yellow-500 hover:bg-yellow-700',
  'bg-green-500 hover:bg-green-700'
];

const selectAnswer = (isCorrect) => {
  if (answerStatus.value !== null) return;
  if (isCorrect) {
    answerStatus.value = 'correct';
    correctAnswers.value++;
  } else {
    answerStatus.value = 'wrong';
    wrongAnswers.value++;
  }
};

const nextQuestion = () => {
  currentQuestionIndex.value++;
  answerStatus.value = null;
};
</script>

<template>
     
    <div class="max-w-xl mx-auto mt-1 p-5">
       
      <div v-if="currentQuestionIndex < questions.length">
        <div class="mt-20 text-center font-bold">
          {{ questions[currentQuestionIndex].question }}
        </div>
        <div :class="{
            'bg-green-500': answerStatus === 'correct', 
            'bg-red-500': answerStatus === 'wrong',
            'bg-gray-500': answerStatus === null
          }" 
          class="p-20  text-white font-bold text-center text-3xl"
        >
          UFPSO
        </div>
       
        <div class="grid grid-cols-2 gap-4 mt-5">
          <button
            v-for="(option, index) in questions[currentQuestionIndex].options"
            :key="index"
            @click="selectAnswer(option.correct)"
            class="p-3 rounded text-white"
            :class="buttonClasses[index]"
          >
            {{ option.text }}
          </button>
        </div>
        <button 
          v-if="answerStatus !== null" 
          @click="nextQuestion" 
          class="mt-5 p-3 bg-blue-500 text-white rounded"
        >
          Siguiente
        </button>
      </div>
      <div v-else class="text-center">
        <p class="font-bold text-2xl">Resultados</p>
        <p>Aciertos: {{ correctAnswers }}</p>
        <p>Fallos: {{ wrongAnswers }}</p>
      </div>
    </div>
  </template>
  
 
  
  