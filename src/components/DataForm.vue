<script>
export default {
  data() {
    return {
        firstName: '',
        secondName: '',
        result: [],
        message: '',
    }

  },
  methods: {
    onSubmit(){
      if (!this.firstName && !this.secondName) {
        alert('Please fill both boxes to get accurate results');
      } else if (!this.firstName){
        alert("Please fill lady's name")
      } else if (!this.secondName){
        alert("Please fill guys's name")
      }  else {
      let URL = `https://loverapi.herokuapp.com/api/v1/calculate?personA=${this.firstName}&personB=${this.secondName}`
      fetch(URL)
        .then(response => response.json())
        .then(data => {
          const newData = data;
          this.result.push(newData);
          this.message = newData;
          //pushes to localstorage
          localStorage.setItem('resultsArray', JSON.stringify(this.result))
          })


        // search if data exists
         const  history = JSON.parse(localStorage.getItem('resultsArray'))
         console.log(history)
        if ( history.includes('Gloria')) {
          console.log('working')
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
        <label for="first name">Name of Lady/woman is </label>
        <input 
          type="text"
          id="first name"
          name="first name"
          v-model="firstName"
        >
      </div>
      <div>
        <label for="second name">Name of Gentleman/Man is </label>
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
        <h2><span>Love Percentage: </span>{{this.message.result}}</h2>
        <h2><span>Message: </span>{{this.message.message}}</h2>
      </div>
    </form>
  </section>
</template>