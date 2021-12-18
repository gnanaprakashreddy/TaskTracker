<template>
  <div class="register">
    <input type="text" v-model="name" placeholder="Enter Name" />
    <input type="text" v-model="email" placeholder="Enter Email" />
    <input type="password" v-model="password" placeholder="Enter Password" />
    <button v-on:click="SignUp">SignUp</button>
    <p>
      <router-link to="/login">Already a user ?? Login</router-link>
    </p>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "SignUp",
  data() {
    return {
      name: "",
      email: "",
      password: "",
    };
  },
  methods: {
    async SignUp() {
      if (
        this.name.length == 0 ||
        this.email.length == 0 ||
        this.password.length == 0
      ) {
        window.alert("Enter all the fields");
      } else {
        if (this.email.length != 0) {
          var pattern = /^\w+@[a-zA-Z_]+?\.[a-zA-Z]{2,3}$/;
          const temp = this.email.match(pattern);
          if (temp == null) {
            alert("Enter a valid Email");
          } else {
            let result = await axios.post("http://localhost:3000/users", {
              email: this.email,
              password: this.password,
              name: this.name,
            });
            //   console.warn(result);
            if (result.status == 201) {
              localStorage.setItem("user-info", JSON.stringify(result.data));
              this.$router.push({ name: "Login" });
            }
          }
        }
      }
    },
    mounted() {
      let user = localStorage.getItem("user-info");
      if (user) {
        this.$router.push({ name: "Login" });
      }
    },
  },
};
</script>

<style>
.register input {
  width: 300px;
  height: 40px;
  padding-left: 20px;
  display: block;
  margin-bottom: 30px;
  margin-right: auto;
  margin-left: auto;
  border: 1px solid skyblue;
  border-radius: 5px;
}
.register a{
    color : white
}
.register button {
  width: 320px;
  height: 40px;
  margin-bottom: auto;
  margin-right: auto;
  margin-left: auto;
  border: 1px solid green;
  background: green;
  color: #fff;
  cursor: pointer;
  border-radius: 5px;
}
</style>
