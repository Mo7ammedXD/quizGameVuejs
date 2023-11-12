<template>
    <div v-if="startGame" class="QuestionsBody">
      <div class="Questions mt-3">
        <h2>{{ questionNow.question  }} - {{ score }}</h2>
      </div>
      <!-- <button type="button" class="actionGame" @click="startGame">play</button> -->
  
      <div class="container mt-4">
        <div class="row">
          <div class="col-6" v-for="(option, index) in questionNow.options" :key="index">
            <button
            :class="{ trueAnswer: keyAnswer === index, falseAnswer: keyAnswer !== index && keyAnswer !== null, defaultClass: keyAnswer === null }"
              type="button"
              @click="checkAnswer(index)"
              class="choice mb-2"
            :disabled="slected"
            >
              <span>{{ index + 1 }}</span>{{ option }}
            </button>
          </div>
        </div>
      </div>
      <button type="button"   :disabled="!slected"  @click="nextLevel" class="actionGame">exit</button>
    </div>
    <div  v-if="!startGame" class="QuestionsBody">
        <img @click="startGame=!startGame" src="https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExaG05MTlxeTI0MmVraWVpMzRtOWQ1bHRxcjhuODgzN2JzYnhlMGdlbCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9dHM/7YbwTmNlnDr0lrC4lY/giphy.gif" alt="">
    </div>
  </template>

  <script>
import quizjson from '#/quiz.json';
import { computed, onMounted, ref } from 'vue';
import {quizGameUes} from '../../stores/quizGame'
export default {
  setup() {
    const level = ref(0);
    const QuizState = quizGameUes
    const score = ref(0);
    const startGame = ref(false);
    const Questions = quizjson.questions;
    const keyAnswer = ref(null);
    const slected = ref(false);

    function nextLevel() {
      level.value++;
      keyAnswer.value = null;
      slected.value = false;
    }

    function checkAnswer(index) {
      keyAnswer.value = Questions[level.value].correct_answer;
      score.value = index === keyAnswer.value ? score.value + 1 : score.value;
      slected.value = true;
    }


    const questionNow = computed(() => {
      return Questions[level.value];
    });

    onMounted(() => {
       console.log()
    });

    return {
      level,
      score,
      startGame,
      Questions,
      keyAnswer,
      questionNow,
      checkAnswer,
      nextLevel,
      slected,
      QuizState
    };
  },
};
</script>



<style scoped>
.QuestionsBody {
    width: 100%;
    
    color: white;
    background-color: rgb(42 43 47);
    text-align: center;
    /* padding: 3rem; */
}
h1{
    font-size: 3rem;
}
.Questions{

    font-size: 1.4rem;
    background-color: white;
    color: black;
    width: 90%;
    margin: auto;
    padding: 10px;
    border-radius: 18px;
}
.Questions h2 {
    font-size: 1.0rem;
}
.actionGame{
    margin: 10px 0px;
    border-radius: 20px;
    color: white;
    background: greenyellow;
    padding: 0.5rem 1.8rem;
    border: solid white 1px;
}
.choice{
    color: white;
    border-radius: 20px;
    background: greenyellow;
    text-align: start;
    padding: 20px  ;
    width:100%;
}
.choice span{
    margin-right: 10px;
    
    padding: 8px;
    border-radius: 100%;
    text-align: center;
    background: black;
}
.trueAnswer{
    
    background-color: green;
}
.falseAnswer{
    background-color: red ;
}
.QuestionsBody img{
    width: 100%;
    height: 300px;
    object-fit: cover;
}
</style>
