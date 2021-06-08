<template>
  <div class="cats__container">
    <router-link class="nav-btn-home" to="/">
      <img class="nav-btn-home" src="@/assets/045-home.svg" alt="Dog Icon" />
    </router-link>
    <CatBreeds />
  </div>
</template>

<script>
import CatBreeds from "@/components/CatBreeds.vue";

export default {
  name: "Cats",
  components: {
    CatBreeds,
  },
};
</script>

<style scoped lang="less">
.nav-btn-home {
  width: 100px;
  height: 100px;
}
</style>
