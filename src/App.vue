<template>
  <div id="app">
    <h1>TRIVIA CEUTEC</h1>
    <p>
      Score:
      <strong>{{score}}</strong>
    </p>
    <question :currentQuestion="currentQuestion" />
    <button
      :class="{ red: currentUserAnswer === 'True' && currentUserAnswer !== currentQuestionAnswer, 
        green: currentUserAnswer === 'True' && currentUserAnswer === currentQuestionAnswer }"
      @click="submitAnswer('True')"
      class="btn"
    >TRUE</button>
    <button
      :class="{ red: currentUserAnswer === 'False' && currentUserAnswer !== currentQuestionAnswer,
      green: currentUserAnswer === 'True' && currentUserAnswer !== currentQuestionAnswer }"
      @click="submitAnswer('False')"
      class="btn"
    >FALSE</button>
    <button @click="goToNextQuestion" class="btn blue">NEXT QUESTION</button>
  </div>
</template>

<script>
import axios from "axios";
import Question from './components/Question';
export default {
  name: "app",
  data() {
    return {
      questions: [],
      currentQuestionNumber: 0,
      currentUserAnswer: "",
      score: 0
    };
  },
  components: {
    'question': Question,
  },
  computed: {
    currentQuestion() {
      return this.questions[this.currentQuestionNumber] || "";
    },
    currentQuestionAnswer() {
      return this.currentQuestion.correct_answer;
    }
  },
  methods: {
    getQuestions() {
      axios
        .get(
          "https://opentdb.com/api.php?amount=10&difficulty=medium&type=boolean"
        )
        .then(result => {
          this.questions = result.data.results;
        });
    },
    submitAnswer(answer) {
      this.currentUserAnswer = answer;
      if (answer === this.currentQuestionAnswer) {
        this.score += 1;
      }
    },
    goToNextQuestion() {
      this.currentUserAnswer = '';
      this.currentQuestionNumber += 1;
    }
  },
  mounted() {
    this.getQuestions();
  }
};
</script>

<style scoped>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
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
