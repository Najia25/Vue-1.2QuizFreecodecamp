<template>
  <div id="app">
    <Header
    v-bind:numCorrect='numCorrect'
    v-bind:numTotal='numTotal'
     />
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">

          <!-- vue lets pass data variables and methods to its child component by using v-bind with custom attributes -->

          <QuestionBox
          v-if="questions.length"
          v-bind:currentQuestion = "questions[index]"
          v-bind:next = "next"
          v-bind:increment="increment"
         
           />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import QuestionBox from  './components/QuestionBox.vue' 

export default {
  name: 'app',
  components: {
    Header,
    QuestionBox
  },
  data: function(){
    return{
      questions: [],
      index:0,
      numCorrect: 0,
      numTotal:0
    }
  },
  mounted: function(){
  fetch('https://opentdb.com/api.php?amount=10&category=27&type=multiple',{
    method:'get'
  })
  .then((response) =>{
    return response.json();
  }) 
  .then((jsonData) =>{
    this.questions = jsonData.results;
  })
},
methods:{
  // alternative syntax 
  // next:function(){...}
  next() {
    this.index++;
  },

  increment(isCorrect){
    if(isCorrect){
      this.numCorrect++;
    }
     this.numTotal++;
  }

}

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
</style>
