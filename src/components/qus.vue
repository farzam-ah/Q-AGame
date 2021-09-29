<template>
  <div class="bg-light p-5 rounded-lg m-3">
    <h1 style="font-size:1.5em">{{ nextCount +" - " }} {{ cQustion.question }}</h1>
    <hr class="my-4" />
    <ul class="list-group">
      <li
        v-for="(answer, i) in randQ"
        :key="i"
        class="list-group-item "
        @click="changeindex(i)"
        :class="classAnswer(i)">
        {{ answer }}
      </li>
    </ul>

    <button
      class="btn btn-primary btn-lg me-2 mt-4"
      href="#"
      role="button"
      :disabled ="cindex===null || answered"
      @click="submitAnswer"
      >submit</button
    >
    <button class="btn btn-warning btn-lg mt-4" href="#" role="button"
     @click="next" :disabled="answered!==true || totalCount===10"
      >Next</button
    >
    <button v-if="totalCount===10"
      class="btn btn-dark btn-lg mt-4 ms-2" @click="finished">finish</button>
  </div>
</template>

<script>
import _ from "lodash";

export default {
  props: {
    cQustion: Object,
    totalCount:Number,
    next: function() {},
    increment: function() {},
    finished: function() {},
    nextCount:Number,
    
    
  },

  computed: {
    answers() {
      let answers = [...this.cQustion.incorrect_answers];
      answers.push(this.cQustion.correct_answer);
      return answers;
    },
  },
  data() {
    return {
      cindex: null,
      randQ: [],
      correctAnswer: null,
      answered: false,
      

    };
  },
  methods: {
    changeindex(i) {
      this.cindex = i;
    },
    randQuestion() {
      let answers = [
        ...this.cQustion.incorrect_answers,
        this.cQustion.correct_answer,
      ];
      this.randQ = _.shuffle(answers);
      this.correctAnswer = this.randQ.indexOf(this.cQustion.correct_answer);
    },
    submitAnswer() {
      let isCorrect = false;
      if (this.cindex === this.correctAnswer) {
        isCorrect = true;
      }
      this.answered = true;
      this.increment(isCorrect);
    },
    classAnswer(index){
      let addClass='';
      if(!this.answered && this.cindex === index){
          addClass='active';
      }else if(this.answered&&index === this.correctAnswer){
          addClass='bg-success';
      }else if(this.answered&&index === this.cindex &&index !== this.correctAnswer){
        addClass='bg-danger';
        }else{
        addClass='notactive';

        }return addClass;
            
    },
    
  },
  watch: {
    cQustion: {
      immediate: true,
      handler() {
        this.cindex = null;
        this.answered = null;
        this.correctAnswer = null;
        this.randQuestion();
      },
    },
  },
};
</script>

<style scoped>
.list-group-item:hover {
  cursor: pointer;
}
.notactive:hover {
  background-color: #eee;
}
</style>
