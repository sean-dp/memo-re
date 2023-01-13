<template>
  <div class="flex">
    <div>
      <GlobalHeader />
    </div>
  </div>
</template>

<script>
import GlobalHeader from "@/components/GlobalHeader.vue";

export default {
  name: "MyPage",
  components: {
    GlobalHeader,
  },
  created() {
    if (this.$cookies.get("access") === null) {
      this.$router.push("/SignIn");
    }
  },
};
</script>
