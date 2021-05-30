<template>
  <div class="box">
    <b-jumbotron lead="Question">
{{currentQuestion.question}}
<br>
      <p>Anwsers</p>
      <b-button variant="primary" href="#">Anwser </b-button>
    </b-jumbotron>
  </div>
</template>

<style>
.box {
  text-align: center;
}
.chose-button {
  float: left;
}
</style>

<script>
export default {
  props:{
    currentQuestion: Object
  },
}
</script>