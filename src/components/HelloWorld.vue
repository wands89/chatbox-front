
<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Chat Box</h2>
    <ul>
      <li>
        <a href="javascript:void(0);" @click="register"> 注册</a>
      </li>
      <li>
        <a href="javascript:void(0);" @click="login"> 登录 </a>
      </li>
    </ul>
    <!-- <register></register> -->
  </div>
</template>

<script>
import Register from "@/components/Register";
import Login from "@/components/Login";
export default {
  name: "HelloWorld",
  data() {
    return {
      msg: "欢迎来到 jingjie.shen 的 chatbox ",
    };
  },
  methods: {
    register() {
      this.$router.push("Register");
      console.log(this.$router);
    },
    login() {
      this.$router.push("Login");
      console.log(this.$router);
    },
  },
  components: {
    register: Register,
    login: Login
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
