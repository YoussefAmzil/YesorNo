<template>
<div class="all" >
  <div class="img">
  <img src="yes-no-maybe.jpeg" alt="" width="40%" height="10%">
</div>
<div class="box">
  <input type="text"  class="qst" pattern="" placeholder="Ask a Question with Yes or No Answer ?"  v-model="text">
  <center>
    <button @click='getAnswer'>Answer me !!</button>
  </center>
</div>

</div>

</template>

<script>
import axios from 'axios';
import VueSweetalert2 from 'vue-sweetalert2';
export default {
  name: 'HelloWorld',
    data(){ 
    return{
      answer:'',
      text:'',
    }   
  },
  methods:{
   getAnswer(){

     if (this.text==='') {

       this.$swal({
          type: 'error',
        title: 'Oops...',
        text: 'You have to fill the Text Box!'
       })
      
     }else{
          axios.get('https://yesno.wtf/api').then(response=>{
            this.answer= response.data;
            this.$swal({
    		  title: '<h1 >'+this.answer.answer.toUpperCase()+'</h1>',
          html:
            '<img src='+this.answer.image+'>',
          showCloseButton: true,
          showCancelButton: true,
          focusConfirm: false,
        })
          }).catch(error=>{
              console.log(error);
          })
         }

    }
  }
}
</script>

<style scoped>
.all{
}
button{
  
  background-color: #4CAF50; /* Green */
  border: none;
  color: white;
  padding: 12px 22px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
}
.box{
display: inline;
border:  black 0.2px;
float: left;
margin-left: 15%;
width: 70%;
padding: 1.2%;
-moz-box-shadow:    3px 3px 5px 6px #ccc;
  -webkit-box-shadow: 3px 3px 5px 6px #ccc;
  box-shadow:         3px 3px 5px 6px #ccc;
}
.qst{
  width: 100%;
  padding: 12px 20px;
  margin: 8px 0;
  display: inline-block;
  border: 1px solid #ccc;
  border-radius: 8px;
  box-sizing: border-box;
}
.img{
  float: left;
  margin-left: 40%;
}
</style>
