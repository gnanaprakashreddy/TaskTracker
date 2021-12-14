<template>
<div>
<Header/>
<form class="add">
<input type = "text" name = "details" v-model = "task.details" placeholder ="Enter task details"/>
<input type = "date" name  ="date" v-model = "task.date" placeholder = "Enter task date"/>
<button type="button" v-on:click="addTask"> Add New Task </button>
</form>
</div>
</template>

<script>
import Header from './Header.vue'
import axios from 'axios';
export default {
   name: 'AddTask',
   components :{
      Header
   },
   data(){
       return {
           task:{
               details: "",
               date:""
           }
       }
   },
   methods:{
      async addTask(){
           console.warn(this.task);
           const result = await axios.post("http://localhost:3000/tasks",{
               details:this.task.details,
               date:this.task.date
           });
           if(result.status == 201){
               this.$router.push({name:'Home'});
           }
           console.warn("result",result);       }
   }
}
</script>

<style>
.add input{
    width : 300px;
    height : 40px;
    padding-left  : 20px;
    display : block;
    margin: 30px;
    margin-right : auto;
    margin-left : auto;
    border :  1px solid skyblue;
    border-radius: 5px;
    }
.add button{
    width : 320px;
    height :  40px;
    margin-bottom: 40px;
    margin-right : auto;
    margin-left : auto;
    border :  1px solid green;
    background : green;
    color : #fff;
    cursor : pointer;
    border-radius: 5px;
}
</style>