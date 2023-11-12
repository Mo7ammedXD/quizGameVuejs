<template>
<div class="nav-bar">
    <h1>Quiz</h1>
    <p @send-data="getData">Score:{{ scoore }}</p>
</div>
</template>

<script>
import { ref } from 'vue';
import Question from '../body/quizBody.vue';

export default {
  setup() {
    const scoore = ref(0);

    function getData(data) {
        scoore.value = data;
    }

    return {
        scoore,
      getData,
      Question
    };
  }
};
</script>


<style scoped>
.nav-bar {
    width: 100%;
    color: white;
    background-color: greenyellow;
    text-align: center;
    padding: 3rem;
}

h1 {
    font-size: 3rem;
}
</style>
