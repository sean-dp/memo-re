<template>
  <p>{{ image_uri }}</p>
  <div class="wrap">
    <h1>記憶を画像にしよう</h1>
    <div class="innerWrap">
      <p>題名</p>
      <input v-model="title" type="text" class="text" />
      <br />
      <p>キーワード</p>
      <input v-model="keyword" type="text" class="text" />
      <br />
      <p>説明</p>
      <textarea
        v-model="text_uri"
        name=""
        cols="30"
        rows="10"
        class="textarea"
      ></textarea>
      <br />
      <button @click="ImageRequest()">画像を作成</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { API_SERVER, AI_SERVER } from "@/assets/config.js";

export default {
  data() {
    return {
      user: 1,
      title: "",
      keyword: "",
      text_uri: "",
      image_uri: "",
      is_public: true,
    };
  },
  name: "CreateImage",
  components: {},
  methods: {
    ImageRequest() {
      const requestBody = {
        user_id: this.user,
        keyword: this.keyword,
      };
      //画像生成
      //   axios.post(import.meta.env.VITE_API_SERVER + "/users/signin", requestBody)
      axios
        .post(AI_SERVER + "/ai/debug", requestBody)
        .then((response) => {
          this.image_uri = response.data.img_file;
          //登録
          const requestBody2 = {
            user: this.user,
            title: this.title,
            keyword: this.keyword,
            text_uri: this.text_uri,
            image_uri: this.image_uri,
            is_public: this.is_public,
          };
          axios
            .post(
              API_SERVER + "/api/v1/brains/" + this.user + "/",
              requestBody2
            )
            .then(() => {
              console.log("成功");
            })
            .catch((e) => {
              console.log(e);
            });
        })
        .catch((e) => {
          console.log(e);
          console.log("失敗");
        });
    },
  },
};
</script>

<style scoped>
h1 {
  font-size: 22px;
  text-align: center;
  margin: 40px;
}
.wrap {
  width: 510px;
  height: 610px;
  margin: 0 auto;
  border: solid 2px #000;
}

.innerWrap {
  width: 420px;
  margin: 0 auto;
}

.text {
  width: 420px;
  height: 40px;
  border: solid 2px #000;
  margin-bottom: 20px;
}

.textarea {
  width: 420px;
  height: 130px;
  border: solid 2px #000;
  margin-bottom: 20px;
}

button {
  float: right;
  color: #fff;
  background: #6d8dff;
  width: 160px;
  height: 54px;
  text-align: center;
  border-radius: 5px;
}
</style>
