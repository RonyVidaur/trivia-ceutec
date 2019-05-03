<template>
    <div class="question-container">
      <p v-html="currentQuestion.question"></p>
    </div>  
</template>

<script>
export default {
  name: 'Question',
  props: {
    currentQuestion: {
      type: Object,
      required: false,
    }
  }
}
</script>


<style>
.question-container {
  background: white;
  border-radius: 20px;
  border: 2px solid #ff6505;
  padding: 10px;
  margin: 10px 60px;
}
</style>
