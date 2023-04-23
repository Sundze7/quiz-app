<script setup>
import { ref, computed } from "vue";

const questions = ref([
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
]);
const quizCompleted = ref(false);
const currentQuestion = ref(0);
const score = computed(() => {
  let value = 0;
  questions.value.map((q) => {
    if (q.selected != null && q.selected == q.answer) {
      console.log("correct");
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

const setAnswer = (e) => {
  questions.value[currentQuestion.value].selected = e.target.value;
  e.target.value = null;
};

const NextQuestion = () => {
  if (currentQuestion.value < questions.value.length - 1) {
    currentQuestion.value++;
    return;
  }
  quizCompleted.value = true;
};
</script>

<template>
  <main class="app">
    <h1>The Quiz</h1>

    <section class="quiz" v-if="!quizCompleted">
      <div class="quiz-info">
        <span class="question">{{ getCurrentQuestion.question }}</span>
        <span class="score"> Score {{ score }}/{{ questions.length }}</span>
      </div>

      <div class="options">
        <label
          v-for="(option, index) in getCurrentQuestion.options"
          :key="index"
          :class="` option ${
            getCurrentQuestion.selected == index
              ? index == getCurrentQuestion.answer
                ? 'correct'
                : 'wrong'
              : ''
          } ${
            getCurrentQuestion.selected != null &&
            index != getCurrentQuestion.selected
              ? 'disabled'
              : ''
          }`"
        >
          <input
            type="radio"
            :name="getCurrentQuestion.index"
            :value="index"
            v-model="getCurrentQuestion.selected"
            :disabled="getCurrentQuestion.selected"
            @change="setAnswer"
          />
          <span>{{ option }}</span>
        </label>
      </div>

      <button @click="NextQuestion" :disabled="!getCurrentQuestion.selected">
        {{
          getCurrentQuestion.index == questions.length - 1
            ? "Finish"
            : getCurrentQuestion.selected == null
            ? "select an option"
            : "Next Question"
        }}
      </button>
    </section>

    <section v-else>
      <h2>You have finished the quiz!</h2>
      <p>Your Score is {{ score }}/{{ questions.length }}</p>
    </section>
  </main>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Montserrat", sans-serif;
}

body {
  background: #271c36;
  color: #fff;
}

.app {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 2rem;
  min-height: 100vh;
}

h1 {
  font-size: 2rem;
  margin-bottom: 2rem;
}

.quiz {
  background-color: #382a4b;
  padding: 1rem;
  width: 100%;
  max-width: 640px;
}

.quiz-info {
  display: flex;
  justify-content: space-between;
  margin-bottom: 1rem;
}

.quiz-info .question {
  color: #8f8f8f;
  font-size: 1.25rem;
}

.quiz-info .score {
  color: #fff;
  font-size: 1.25rem;
}

.options {
  margin-bottom: 1rem;
}

.option {
  padding: 1rem;
  display: block;
  background-color: #271c36;
  margin-bottom: 0.5rem;
  border-radius: 0.5rem;
  cursor: pointer;
}
.option:hover {
  background-color: #2d213f;
}
.option.correct {
  background-color: #2cce7d;
}
.option.wrong {
  background-color: #ff5a5f;
}
.option:last-of-type {
  margin-bottom: 0;
}
.option.disabled {
  opacity: 0.5;
}
.option input {
  display: none;
}
button {
  appearance: none;
  outline: none;
  border: none;
  cursor: pointer;
  padding: 0.5rem 1rem;
  background-color: #2cce7d;
  color: #2d213f;
  font-weight: 700;
  text-transform: uppercase;
  font-size: 1.2rem;
  border-radius: 0.5rem;
}
button:disabled {
  opacity: 0.5;
}
h2 {
  font-size: 2rem;
  margin-bottom: 2rem;
  text-align: center;
}
p {
  color: #8f8f8f;
  font-size: 1.5rem;
  text-align: center;
}
</style>
