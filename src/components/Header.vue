<template>
  <div>
    <h1 class="title" >Quiz APP</h1>
    <b-nav tabs >
      <b-nav-item class="indic"> Correct: <span style="color:green;">{{correctCount}}</span></b-nav-item>
      <b-nav-item class="indic">Incorrect: <span style="color:red;">{{incorrectCount}}</span></b-nav-item>
    </b-nav>
  </div>
</template>

<style scoped>
  .title{
    color: teal;
    text-align: center;
  }
  .indic{
    font-size: 25px;
  }

</style>

<script>
export default{
  props: {
  },
  data() {
    return {
    incorrectCount: 0,
    correctCount: 0
    }
  },
  mounted() {
    this.$root.$on('correct', data => {
        this.correctCount += data;
    });
    this.$root.$on('incorrect', data => {
        this.incorrectCount += data;
    });
}
}
</script>
