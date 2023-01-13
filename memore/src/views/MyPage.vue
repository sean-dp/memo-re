<template>
  <div class="flex">
    <div class="fixedGlobal">
      <GlobalHeader />
    </div>
    <div>
      <div></div>
      <div class="flex">
        <h2>すべての記憶</h2>
        <button>申請したい記憶を選択</button>
      </div>
      <div class="imageWrap">
        <div
          v-for="image in data"
          v-bind:key="image"
          class="imageBox"
          @click="ImageView(image.id, image.user)"
        >
          <!-- <p>{{ image.title }}</p>
          <p>{{ image.text_uri }}</p> -->
          <div class="myPageImage">
            <img :src="'/media/brain/' + image.image_uri" alt="画像" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { API_SERVER } from "@/assets/config.js";
import GlobalHeader from "@/components/GlobalHeader.vue";

export default {
  name: "MyPage",
  components: {
    GlobalHeader,
  },
  data() {
    return {
      data: [],
    };
  },
  methods: {
    Created: async function () {
      const token = this.$cookies.get("access");
      const id = localStorage.getItem("id");
      console.log(token);
      await axios
        .get(API_SERVER + "/api/v1/brains/" + id, {
          headers: { Authorization: "JWT " + token },
        })
        .then((response) => {
          this.data = response.data;
          console.log(this.data);
          return;
        })
        .catch((e) => {
          console.log(e);
          return;
        });
    },
    ImageView(noteId, user) {
      localStorage.setItem("noteUserId", user);
      localStorage.setItem("noteId", noteId);
      this.$router.push("/imageView");
    },
  },
  created() {
    if (this.$cookies.get("access") === null) {
      this.$router.push("/SignIn");
      return;
    }
    this.Created();
  },
};
</script>
<style scoped>
.imageWrap {
  width: calc(100vw - 180px);
  display: flex;
  /* justify-content: space-between; */
  flex-wrap: wrap;
}
.imageBox {
  margin: 20px;
}
.myPageImage {
  width: 180px;
}
.myPageImage img {
  width: 100%;
}
</style>
