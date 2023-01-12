<template>
  <div class="wrap">
    <div class="image"><img src="@/assets/logo.png" alt="ロゴ" /></div>
    <div class="side"></div>
  </div>
</template>

<script>
// @ is an alias to /src
export default {
  name: "GlobalHeader",
  components: {},
};
</script>
<style scoped>
.wrap {
  position: relative;
  width: 170px;
  height: 100vh;
  background: #515058;
}
.image {
  width: 80px;
  height: 80px;
  margin: 0 auto;
}
img {
  width: 100%;
}
.side {
  position: absolute;
  top: 0;
  left: 170px;
  width: 100px;
  height: 100vh;
  background: #f00;
}
</style>
