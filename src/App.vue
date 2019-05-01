<template>
  <div id="app">
    <h1>TRIVIA CEUTEC</h1>
    <div class="question-container">
      <p v-html="currentQuestion"></p>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'app',
  data() {
    return {
      questions: [],
      currentQuestionNumber: 0,
      currentUserAnswer: '',
    };
  },
  computed: {
    currentQuestion() {
      return this.questions[this.currentQuestionNumber].question;
    }
  },
  mounted() {
    axios.get('https://opentdb.com/api.php?amount=10&difficulty=medium&type=boolean')
      .then((result) => {
        this.questions = result.data.results;
      });
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.red {
  background-color: #d20639 !important;
}

.green {
  background-color: #558c1d !important;
}

h1 {
  color: #2c3e50;
}

h1 span {
  color: #ff6505;
}

.question-container {
  background: white;
  border-radius: 20px;
  border: 2px solid #ff6505;
  padding: 10px;
  margin: 10px 60px;
}

.btn {
  outline: none;
  padding: 5px;
  background-color: #558fdb;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 20px;
  margin: 5px;
  color: #fff;
}

.blue {
  background-color: #51bba8;
}
</style>
