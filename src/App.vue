<template>
  <div id="app" class="main">
    <!-- <main> -->
    <section class="glass">
      <Header 
      />
      <b-container class="question-container">
        <b-row>
            <QuestionBox 
              v-if="questions.length"
              :currentQuestion="questions[index]"
            />
        </b-row>
        <b-row>
          <div>
            <br><br><br>
      <b-button @click="prev" class="prev-button" variant="success" href="#">Prev</b-button>
      <b-button @click="next" class="next-button" variant="success" href="#">Next</b-button>
          </div>
        </b-row>
      </b-container>
    </section>
    <!-- </main> -->
    <div class="circle1"></div>
    <div class="circle2"></div>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import QuestionBox from "./components/QuestionBox.vue";

export default {
  name: "App",
  components: {
    Header,
    QuestionBox,
  },
  data() {
    return {
      questions:[],
      index:0,
      correctCount: 0,
      incorrectCount: 0
    }
  },
  methods: {
    next(){
      if(this.index < this.questions.length -1){
        this.index ++
      }
    },
    prev(){
      if(this.index > 0){
        this.index --
      }
    }
  },
  mounted: function() {
    fetch('https://opentdb.com/api.php?amount=5&difficulty=easy&type=multiple',{
      method: 'get',

   }).then((response) =>{
     return response.json();
   }).then((jsonData) =>{
     this.questions = jsonData.results;
     console.log(this.questions);
   })
  },
};
</script>


<style>
@import "https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;700&display=swap";

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

h1 {
  color: #426696;
  font-weight: 600;
  font-size: 3rem;
  opacity: 0.8;
}
h2, p {
  color: #658ec6;
  font-weight: 500;
  opacity: 0.8;
}

h3 {
  color: #426696;
  font-weight: 600;
  opacity: 0.8;
}

.main {
  font-family: "Poppins", sans-serif;
  min-height: 100vh;
  background: linear-gradient(to right top, #65dfc9, #6cdbeb);
  display: flex;
  align-items: center;
  justify-content: center;
}

.glass {
  background: white;
  min-height: 80vh;
  width: 40%;
  background: linear-gradient(
    to right bottom,
    rgba(255, 255, 255, 0.7),
    rgba(255, 255, 255, 0.3)
  );
  border-radius: 2rem;
  z-index: 2;
  backdrop-filter: blur(2rem);
  /* display: flex; */
}
.circle1, .circle2 {
  background: white;
  background: linear-gradient(
    to right bottom,
    rgba(255, 255, 255, 0.8),
    rgba(255, 255, 255, 0.3)
  );
  height: 20rem;
  width: 20rem;
  position: absolute;
  border-radius: 50%;
}

.circle1 {
  top: 5%;
  right: 17%;
}
.circle2 {
  bottom: 5%;
  left: 18%;
}
.dashboard {
  flex: 1;
  flex-direction: column;
  align-items: center;
  justify-content: space-evenly;
  text-align: center;
  background: linear-gradient(
    to right bottom,
    rgba(255, 255, 255, 0.7),
    rgba(255, 255, 255, 0.3)
  );
  border-radius: 2rem;
}
.link {
  margin: 2rem 0rem;
}
.link h2 {
  padding: 0rem 2rem;
}

.games {
  flex: 2;
}

.pro {
  background: linear-gradient(to right top, #65dfc9, #6cdbeb);
  border-radius: 2rem;
  color: white;
  padding: 1rem;
  position: relative;
}

.pro img {
  position: absolute;
  top: -10%;
  right: 10%;
}
.pro h2 {
  width: 40%;
  color: white;
  font-weight: 600;
}

/* GAMES */
.status {
  margin-bottom: 3rem;
}

.status input {
  background: linear-gradient(
    to right bottom,
    rgba(255, 255, 255, 0.7),
    rgba(255, 255, 255, 0.3)
  );
  border: none;
  width: 50%;
  padding: 0.5rem;
  border-radius: 2rem;
}

.games {
  margin: 5rem;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
}

.card {
  display: flex;
  background: linear-gradient(
    to left top,
    rgba(255, 255, 255, 0.8),
    rgba(255, 255, 255, 0.5)
  );
  border-radius: 1rem;
  margin: 2rem 0rem;
  padding: 2rem;
  box-shadow: 6px 6px 20px rgba(122, 122, 122, 0.212);
  justify-content: space-between;
}

.progress {
  background: linear-gradient(to right top, #65dfc9, #6cdbeb);
  width: 100%;
  height: 25%;
  border-radius: 1rem;
  position: relative;
  overflow: hidden;
}
.progress::after {
  content: "";
  width: 100%;
  height: 100%;
  background: rgb(236, 236, 236);
  position: absolute;
  left: 60%;
}
.card-info {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.percentage {
  font-weight: bold;
  background: linear-gradient(to right top, #65dfc9, #6cdbeb);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.question-container{
  background: linear-gradient(
    to left top,
    rgba(253, 251, 251, 0.8),
    rgba(199, 243, 241, 0.5)
  );
  border-radius: 1rem;
  margin: 3.5rem -0.2rem;
  padding: 2rem;
  box-shadow: 6px 6px 20px rgba(122, 122, 122, 0.212);
  justify-content: space-between;
}

.next-button {
  display: block;
  width: 15%;
  float: right;
background-color: #299797;
}

.prev-button {
  display: block;
  width: 15%;
  float: left;
background-color: #299797;
}
</style>
