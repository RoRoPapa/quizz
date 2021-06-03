<template>
  <div class="box">
    <b-jumbotron lead="Question">
      <span class="question-text">
        {{ currentQuestion.question }}
      </span>
      <div>
        <br />
        <p>Anwsers</p>
        <b-form-group class="form-questions">
          <b-form-radio
            v-model="selected"
            :value="question"
            class="option"
            v-for="(question, index) in allAnwsers"
            :key="index"
          >
            {{ question }}
          </b-form-radio>
        </b-form-group>
      </div>
      <br />
      <b-button @click="validAnwser" variant="primary" href="#"
        >Anwser
      </b-button>
    </b-jumbotron>
<div>
  <b-button v-b-modal.modal-no-backdrop ref="resultModal" style="display:none; "></b-button>
  <b-modal id="modal-no-backdrop" hide-backdrop content-class="shadow" title="" :hide-footer="true" :hide-header="true" style="align-items: center; text-aling:center;">
    <img :src="link">
    <h1>{{result}}</h1>
  </b-modal>
</div>

  </div>
</template>

<style>
.box {
  text-align: center;
}
.chose-button {
  float: left;
}
.form-questions {
  margin-left: auto;
  margin-right: 0;
}
.question-text {
  height: 60px;
  display: block;
}
</style>

<script>
export default {
  props: {
    currentQuestion: Object,
  },
  data() {
    return {
      selected: "",
      showModal: false,
      index: 0,
      link:'',
      result:'',
      incorrectCount: 0,
      correctCount:0
    };
  },
  computed: {
    allAnwsers() {
      let totalAnwsers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer];
      return totalAnwsers.sort(() => Math.random() - 0.4);
    },
  },
  methods: {
    validAnwser() {
      let mod = '';
      if(this.selected){
      if (this.selected == this.currentQuestion.correct_answer) {
        mod = 'happy' ;
        this.result = "Yep";
        this.$root.$emit('correct', 1);
      }else{
        mod = 'sad';
        this.result = "Nop";
        this.$root.$emit('incorrect', 1);
      }
    let imgUrl = 'http://localhost:8081/api/cat/img/'+mod;
    var timestamp = new Date().getTime();  
    var queryString = "?t=" + timestamp;    
    this.link= imgUrl + queryString;    
    this.$refs.resultModal.click()
      }
    },
  },
};
</script>