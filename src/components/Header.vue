<template>
<div class="container">
<router-link to="/">Home</router-link>
<router-link to="/task">Add Task</router-link>
<a v-on:click="logout" href="#" style="float:right;">Logout</a>
</div>
</template>
<script>
export default {
    name:'Header',
    methods :{
        logout(){
            localStorage.clear();
            this.$router.push({name:'Login'})
        }
    }
}
</script>
<style scoped>
.container{
    background-color : green;
    overflow : hidden;
    border-radius: 5px;
}
.container a{
    float : left;
    color : #f2f2f2f2;
    padding : 14px 16px;
    text-align:center;
    font-size :17px;
    text-decoration : none;
    margin-right : 5px;
}
.container a:hover{
    background :#ddd;
    color : green;
}   

</style>