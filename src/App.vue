<template>
  <div>
    <loading
      class="d-flex justify-content-between align-content-between"
      :isLoading="isLoading"
    />
    <div class="main" v-if="!isLoading">
      <navbar
        :correctCount="correctCount"
        :totalCount="totalCount"
        class="overflow-hidden"
      />

      <div class="row d-flex justify-content-center overflow-hidden w-100">
        <qus
          v-if="questionlist.length"
          :cQustion="questionlist[index]"
          :next="next"
          class="col-md-5 "
          :increment="increment"
          :totalCount="totalCount"
          :nextCount="nextCount"
          :finished="finished"
        />
      </div>
    </div>
  </div>
</template>

<script>
import navbar from "./components/navbar.vue";
import qus from "./components/qus.vue";
import loading from "./components/loading.vue";

export default {
  name: "App",
  components: {
    navbar,
    qus,
    loading,
  },
  data() {
    return {
      questionlist: [],
      index: 0,
      correctCount: 0,
      totalCount: 0,
      isLoading: true,
      nextCount:1,
      finishClick:false,
      
    };
  },
  methods: {
    next() {
      if (this.index < 9) {
        this.index++;
        this.nextCount++;
      }
    },
    increment(isCorrect) {
      if (isCorrect) {
        this.correctCount++;
      }
      this.totalCount++;
    },
    finished() {
      if(this.index===10){this.finishClick=true;}
      
      
    }
  },
  mounted: function() {
    fetch("https://opentdb.com/api.php?amount=10&category=10", {
      method: "get",
    })
      .then((respnse) => {
        return respnse.json();
      })
      .then((result) => {
        this.questionlist = result.results;
      });
    setTimeout(() => {
      this.isLoading = false;
    }, 3000);
  },
};
</script>

<style></style>
