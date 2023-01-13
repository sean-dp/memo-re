<template>
  <div></div>
</template>

<script>
import axios from "axios";
import { API_SERVER } from "@/assets/config.js";
export default {
  name: "ImageView",
  data() {
    return {
      data: [],
    };
  },
  components: {},
  methods: {
    ImageData: async function () {
      const noteId = localStorage.getItem("noteId");
      const noteUserId = localStorage.getItem("noteUserId");
      this.$cookies.remove("noteId");
      this.$cookies.remove("noteUserId");
      const token = this.$cookies.get("access");
      await axios
        .post(API_SERVER + "/api/v1/brains/" + noteUserId + "/" + noteId, {
          headers: { Authorization: "JWT " + token },
        })
        .then(() => {
          console.log("成功");
          return;
        })
        .catch((e) => {
          console.log(e);
          // this.$router.push({ name: "myPage" });
          return;
        });
    },
  },
  created() {
    this.ImageData();
  },
};
</script>

<style scoped></style>
