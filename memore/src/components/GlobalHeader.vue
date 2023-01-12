<template>
  <div class="gl-wrap">
    <div class="gl-global">
      <div class="image"><img src="@/assets/logo.png" alt="ロゴ" /></div>
      <ul>
        <li><router-link to="/MyPage">Profile</router-link></li>
        <li><router-link to="/CreateImage">Create</router-link></li>
        <li @click="GlobalSide()">Friend</li>
        <li @click="GlobalSide()">Search</li>
        <li @click="GlobalSide()">Notice</li>
      </ul>
      <p class="logout" @click="Logout()">Logout</p>
    </div>
    <div class="side" v-if="globalFlag"></div>
  </div>
</template>

<script>
// @ is an alias to /src
export default {
  name: "GlobalHeader",
  components: {},
  data() {
    return {
      globalFlag: false,
      sideBar: "",
    };
  },
  methods: {
    GlobalSide() {
      this.globalFlag = !this.globalFlag;
      return;
    },
    Logout() {
      this.$cookies.remove("access");
      this.$router.push('/SignIn');
      return;
    },
  }
};
</script>
<style scoped>
.gl-wrap {
  position: relative;
  width: 170px;
  height: 100vh;
  background: #515058;
}
.gl-global {
  height: 100%;
  position: relative;
  padding-top: 100px;
  color: #fff;
  font-size: 18px;
}
.gl-global ul {
  margin-top: 80px;
  margin-left: 56px;
}
.gl-global li {
  margin-bottom: 16px;
}
.image {
  width: 80px;
  height: 80px;
  margin: 0 auto;
}
img {
  width: 100%;
}
.gl-global p {
  position: absolute;
  bottom: 100px;
  left: 56px;
}
.side {
  position: absolute;
  top: 0;
  left: 170px;
  z-index: 5;
  width: 260px;
  height: 100vh;
  background: #CCC6C6;
}
</style>
