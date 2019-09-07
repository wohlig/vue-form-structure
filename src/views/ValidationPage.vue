<template>
  <div>
    <div class="main-background">
      <!--  -->
      <Header></Header>
      <AllForms></AllForms>
      <!--  -->
    </div>
  </div>
</template>
<script>
import Header from "@/components/Header.vue";
import AllForms from "@/components/AllForms.vue";
export default {
  components: {
    Header,
    AllForms
  }
};
</script>
<style lang="scss">
.main-background {
  background-image: linear-gradient(
      rgba(223, 39, 230, 0.767),
      rgba(23, 39, 185, 0.755)
    ),
    url("~@/assets/computer.jpg");
  height: 100vh;
  position: fixed;
  width: 100%;
  background-repeat: no-repeat;
  background-size: cover;
  overflow-y: scroll;
}
</style>
