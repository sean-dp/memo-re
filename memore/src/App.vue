<template>
  <div>
    <div v-if="flag" class="header">
      <GlobalHeader />
      <div>
        <router-view />
      </div>
    </div>
    <div v-if="!flag" class="header">
      <router-view />
    </div>
  </div>
</template>

<script>
import GlobalHeader from "@/components/GlobalHeader.vue";

export default {
  data() {
    return {
      flag: true,
      path: "",
    };
  },
  name: "MyPage",
  components: {
    GlobalHeader,
  },
  created() {
    console.log("開始");
    this.path = this.$route.path;
    console.log(this.$route.path);
    if (this.path === "/signIn") {
      this.flag = false;
    }
  },
  reload() {
    console.log("開始");
    this.path = this.$route.path;
    console.log(this.$route.path);
    if (this.path === "/signIn") {
      this.flag = false;
    }
  },
};
</script>

<style scoped>
@import "./css/destyle.css";

.header {
  display: flex;
}
</style>
