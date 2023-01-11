<template>
  <div class="wrap">
    <div></div>
    <h1>サインアップ</h1>
    <div>
      <p>メールアドレス</p>
      <input v-model="email" type="text" class="text" />
      <br />
      <p>パスワード</p>
      <input v-model="password" type="password" class="text" />
      <br />
      <button @click="SignUp()">新規登録</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { API_SERVER } from "@/assets/config.js";
export default {
  name: "SignIn",
  components: {},
  data() {
    return {
      password: null,
      email: null,
    };
  },
  methods:{
    SignIn(){
      const requestBody = {
        password: this.password,
        email: this.email,
      }
      axios.post(API_SERVER + "/api/v1/auth/jwt/create/", requestBody)
        .then((response) => {
          console.log("成功")
        })
        .catch((e) => {
            //エラー回避用
        });
    }
  }

};
</script>

<style scoped></style>