<template>
  <h2>hello world</h2>
</template>

<script setup>
import { ref, computed } from "vue";

const questions = ref([
  [
    {
      question: "What is the capital of Australia?",
      options: ["Sydney", "Melbourne", "Canberra", "Brisbane"],
      answer: 2,
      selected: null,
    },
    {
      question: "Who is the author of the Harry Potter series?",
      options: [
        "J.K. Rowling",
        "Stephenie Meyer",
        "Suzanne Collins",
        "Veronica Roth",
      ],
      answer: 0,
      selected: null,
    },
    {
      question: "What is the largest planet in our solar system?",
      options: ["Venus", "Saturn", "Jupiter", "Mars"],
      answer: 2,
      selected: null,
    },
    {
      question: "What is the largest organ in the human body?",
      options: ["Heart", "Liver", "Brain", "Skin"],
      answer: 3,
      selected: null,
    },
    {
      question: "What is the currency of Japan?",
      options: ["Yen", "Dollar", "Euro", "Pound"],
      answer: 0,
      selected: null,
    },
    {
      question: "What is the smallest country in the world?",
      options: ["Monaco", "San Marino", "Vatican City", "Liechtenstein"],
      answer: 2,
      selected: null,
    },
    {
      question: "What is the chemical symbol for gold?",
      options: ["Ag", "Au", "Cu", "Fe"],
      answer: 1,
      selected: null,
    },
    {
      question: "Which language is spoken in Brazil?",
      options: ["Spanish", "Portuguese", "French", "Italian"],
      answer: 1,
      selected: null,
    },
    {
      question: "Who invented the telephone?",
      options: [
        "Alexander Graham Bell",
        "Thomas Edison",
        "Nikola Tesla",
        "Guglielmo Marconi",
      ],
      answer: 0,
      selected: null,
    },
    {
      question: "What is the largest animal on Earth?",
      options: ["Elephant", "Blue Whale", "Giraffe", "Hippopotamus"],
      answer: 1,
      selected: null,
    },
  ],
]);
const quizCompleted = ref(false);
const currentQuestion = ref(0);
const score = computed(() => {
  let value = 0;
  questions.value.map((q) => {
    if (q.selected == q.answer) {
      value++;
    }
  });
  return value;
});

const getCurrentQuestion = computed(() => {
  let question = questions.value[currentQuestion.value];
  question.index = currentQuestion.value;
  return question;
});

const setAnswer = (evt) => {
  questions.value[currentQuestion.value].selected = evt.target.value;
  evt.target.value = null;
};

const NextQuestion = () => {
  if (currentQuestion.value < questions.value.length - 1) {
    currentQuestion.value++;
  } else {
    quizCompleted.value = true;
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Montserrat", sans-serif;
}

body {
  background: #271c34;
  color: #fff;
}
</style>
