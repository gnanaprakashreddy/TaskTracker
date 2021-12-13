<template>
<div class="container">
<h1> Task List</h1>
<Header/>
<table border="1">
<tr>
<td><b>Task Name</b></td>
<td><b> Date of The Task</b></td>
<td><b> Action</b></td>
</tr>
<tr v-for="list in tasks" :key="list.id">
<td>
{{list.details}}
</td>
<td>
{{list.date}}
</td>
<td><button v-on:click="deleteTask(list.id)">Delete</button></td>
</tr>
</table>
</div>
</template>

<script>
import Header from './Header.vue'
import axios from 'axios';
export default {
   name: 'Home',
   components :{
      Header
   },
   data(){
      return{
         name:'',
         tasks:[],
      }
   },
   methods:{
       async deleteTask(id){
            let result = await axios.delete("http://localhost:3000/tasks/"+id);
           console.log(result.status);
           window.location.reload();

        }
   },
     async mounted(){
          let user = localStorage.getItem('user-info');
          console.log(user);
          this.name = JSON.parse(user).name;
          console.warn(this.name);
          if(!user){
              this.$router.push({name:'SignUp'})
          }
          let result = await axios.get("http://localhost:3000/tasks");
          console.warn(result);
          this.tasks = result.data;
          console.warn(this.tasks);
      }
}
</script>
<style scoped>
.container button{
   background :red;
   color :white;
}
.container table{
   height : 100%;
   width : 100%;
}
</style>