<template>
  <div class="wrap">
    <div></div>
    <h1>サインアップ</h1>
    <div>
      <p>ユーザー名</p>
      <p>{{ error.username }}</p>
      <input v-model="username" type="text" class="text" />
      <br />
      <p>メールアドレス</p>
      <p>{{ error.email }}</p>
      <input v-model="email" type="text" class="text" />
      <br />
      <p>パスワード</p>
      <input v-model="password" type="password" class="text" />
      <br />
      <p>確認用パスワード</p>
      <p>{{ error.password }}</p>
      <input v-model="checkpass" type="password" class="text" />
      <br />
      <button @click="SignUp()">新規登録</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { API_SERVER } from "@/assets/config.js";
export default {
  name: "SignUp",
  components: {},
  data() {
    return {
      username: null,
      password: null,
      checkpass: null,
      email: null,
      signUp:[],
      error:[],
    };
  },
  methods:{
    SignUp(){
      const requestBody = {
        email: this.email,
        username: this.username,
        password: this.password,
      }
      axios.post(API_SERVER + "/api/v1/auth/users/", requestBody)
        .then((response) => {
          this.signUp = response.data;
          console.log(this.signUp);
        })
        .catch((e) => {
          this.error = e.response.data;
          console.log(e);
          console.log(this.error);
        });
    }
  }

};
</script>

<style scoped></style>
