<template>
  <div class="login">
  <input type = "text" v-model = "email"  placeholder= "Enter Email"/>
  <input type = "password" v-model = "password" placeholder = "Enter Password"/>
  <button v-on:click="Login"> Login </button>
  <p>
  <router-link to='/'>New User?? SignUp</router-link>
  </p>
  </div>
</template>

<script>

import axios from 'axios'
export default {
  name: 'Login',
  data(){
      return {
          email : "",
          password: ""
      }
  },
  methods:{
     async Login(){
          let result = await axios.get(`http://localhost:3000/users?email=${this.email}&password=${this.password}`)
        //   console.warn(result);
          if(result.status == 200 && result.data.length>=1){  
              localStorage.setItem("user-info",JSON.stringify(result.data));
              this.$router.push({name:'Home'})
          }
          else{
              alert("Please register first..!")
          }
      },
  }
}
</script>

<style>
.login input{
    width : 300px;
    height : 40px;
    padding-left  : 20px;
    display : block;
    margin-bottom: 30px;
    margin-right : auto;
    margin-left : auto;
    border :  1px solid skyblue;
    border-radius: 5px;
    }
.login a{
    color : white
}
.login button{
    width : 320px;
    height :  40px;
    margin-bottom: auto;
    margin-right : auto;
    margin-left : auto;
    border :  1px solid green;
    background : green;
    color : #fff;
    cursor : pointer;
     border-radius: 5px;
}
</style>
