<template>
<div class="container">
<Header/>
<table id="tb">
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
          console.log("In Home Page");
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
   border: 5px;
}
.container table{
   margin-top: 5px;
   height : 100%;
   width : 100%;
   border : none;
}
#tb{
   border: none
}
</style>