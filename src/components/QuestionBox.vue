<template>
  <div class="question-box-container">
    <b-jumbotron>
      <template v-slot:lead>
        {{ currentQuestion.question }}
      </template>

      <hr class="my-4">

      <b-list-group>
        <b-list-group-item
        v-for="(answer,index) in answers" 
        v-bind:key="index"
        @click.prevent="selectAnswer(index)"
        :class="[selectedIndex === index ? 'selected' : '']"
        >
          {{ answer }}
        </b-list-group-item>
      </b-list-group>
    
      <b-button variant="primary" href="#">Submit</b-button>
      <b-button variant="success" href="#" @click="next">Next</b-button>
    </b-jumbotron>
  </div>
</template>
<script>
export default {
  props:{
    currentQuestion: Object,
    next: Function

  },
  data(){
    return{
      selectedIndex: null
    }
  },
  computed:{
    answers(){
      let answers = [...this.currentQuestion.incorrect_answers];
      answers.push(this.currentQuestion.correct_answer);
      return answers;
    }
    
  },

  methods:{
    selectAnswer(index){
      this.selectedIndex = index;
      // console.log(this.selectedIndex);
    }
  }
   
}
</script>

// scoped means the styles written inside the tags are not global tags
// they are only effective for this component

<style scoped>
.list-group{
  margin-bottom:15px;
}

.list-group-item:hover{
  background:#eee;
  cursor: pointer;
}

.btn{
  margin:0 5px;
}

.selected{
  background: lightblue;
}

.correct{
  background: lightgreen;
}

.incorrect{
  background:red;
}

</style>