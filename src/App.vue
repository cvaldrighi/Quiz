<template>
  <div class="ctr"> 
    <transition name="fade" mode="out-in">
      <quiz-questions v-if="questionsAnswered < questions.length" 
      :questions="questions" :questionsAnswered="questionsAnswered" @question-answered="questionAnswered"/>
      <quiz-results v-else :results="results" :totalCorrect="totalCorrect"/>
    </transition>
    <button type="button" class="reset-btn" @click.prevent="reset()" v-if="this.questionsAnswered === questions.length">Reset</button>
  </div>
</template>

<script>
import QuizQuestions from "./components/QuizQuestions.vue"
import QuizResults from "./components/QuizResults.vue"


export default {
  name: 'App',
  components: {
    QuizQuestions,
    QuizResults
  },
  data() {
    return {
      questionsAnswered: 0,
      totalCorrect: 0,
      questions: [
          {
              q: 'Quantos ossos tem o corpo humano?', 
              answers: [
                  {
                      text: '206',
                      is_correct: true
                  },
                  {
                      text: '200',
                      is_correct: false 
                  },
                  {
                      text: '187',
                      is_correct: false 
                  },
                  {
                      text: '213',
                      is_correct: false 
                  }
              ] 
          },
          { 
              q: 'Quantos elementos tem a tabela periódica?', 
              answers: [
                  {
                      text: '98',
                      is_correct: false
                  },
                  {
                      text: '87',
                      is_correct: false 
                  },
                  {
                      text: '118',
                      is_correct: true 
                  },
                  {
                      text: '96',
                      is_correct: false 
                  }
              ] 
          },
          { 
              q: 'Existem quantos países na América do Sul?', 
              answers: [
                  {
                      text: '10',
                      is_correct: false
                  },
                  {
                      text: '12',
                      is_correct: true 
                  },
                  {
                      text: '14',
                      is_correct: false 
                  }
              ] 
          },
      ],
      results: [
          {
              min: 0,
              max: 2,
              title: "Oh oh...",
              desc: "Tente novamente! "
          },
          {
              min: 3,
              max: 3,
              title: "Uhul!!!",
              desc: "Você conseguiu!"
          }
      ]
    }
  },
  methods: {
    questionAnswered(is_correct) {
      if(is_correct) {
        this.totalCorrect++;
      }

      this.questionsAnswered++;
    },
    reset() {
      this.questionsAnswered = 0;
      this.totalCorrect = 0;
    },
  },
}
</script>

