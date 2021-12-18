<template>
  <div>
    <h1>Task List</h1>
    <router-view />
  </div>
</template>

<script>
export default {
  name: "App",
};
</script>

<style>
#app {
  text-align: center;
  color: white;
  margin-top: 60px;
  padding: 1rem;
  background-color: rgb(31, 31, 31);
  margin: 2rem auto;
  width: 50rem;
  max-width: 95%;
  border: 1px solid black;
  border-radius: 10px;
}
</style>
