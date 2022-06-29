<script>
export default {
  data() {
    return {
        firstName: '',
        secondName: '',
        result: [],
        resultsArray: [],
        nameBank: []
    }

  },
  methods: {
    onSubmit(){
      if (!this.firstName && !this.secondName) {
        // return;
        alert('Please fill both boxes to get accurate results');
      } else if (!this.firstName){
        alert("Please fill lady's name")
      } else if (!this.secondName){
        alert("Please fill guys's name")
      }  else {

        this.nameBank.push(this.firstName + '' + this.secondName)
      
        this.getAPIResults()

        // saves searched names in array
        console.log(this.nameBank);
      }
      

    },
    getAPIResults() {
      // sends get request to API
      let result = '';
      if (this.firstName == '' && this.secondName == ''){
        console.log('e get why')
      } else {
      let URL = `https://loverapi.herokuapp.com/api/v1/calculate?personA=${this.firstName}&personB=${this.secondName}`
      fetch(URL)
        .then(response => response.json())
        .then(data => this.result = data)
        console.log(this.result)
      
          this.resultsArray.push(this.result)
          console.log('works')
          console.log(this.resultsArray)
        

        //saves result to localStorage
        if(this.resultsArray = []){
          console.log('wont work')
        } else {
          localStorage.setItem('resultsArray', JSON.stringify(this.resultsArray))
          console.log(this.result)
          console.log(localStorage.getItem('resultsArray'))
        }
      }
    },
    reset() {
        this.firstName = '';
        this.secondName = '';
        this.result = '';
    }
  }
}
  
</script>

<template>
  <section>
    <h1>Love calculator</h1>
    <h2>Fill in the your name and the name of your partner and know your love rate!</h2>
    <form action="" @submit.prevent="onSubmit">
      <div>
        <label for="first name">Name of Lady/woman is {{firstName}}</label>
        <input 
          type="text"
          id="first name"
          name="first name"
          v-model="firstName"
        >
      </div>
      <div>
        <label for="second name">Name of Gentleman/Man is {{secondName}}</label>
        <input 
          type="text"
          id="second name"
          name="second name"
          v-model="secondName"
        >
      </div>
      <div>
        <button type="submit" value="Submit" @click="onSubmit">Calculate</button>
      </div>
      <div>
        <button type="button" value="Resset" @click="reset">Reset</button>
      </div>
      <div>
        <h1>Result:</h1>
        <h2><span>Love Percentage: </span>{{this.result.result}}</h2>
        <h2><span>Message: </span>{{this.result.message}}</h2>
      </div>
    </form>
  </section>
</template>