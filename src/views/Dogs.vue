<template>
  <div class="dogs__container">
    <router-link class="nav-btn" to="/">
      <img class="nav-btn-home" src="@/assets/045-home.svg" alt="Dog Icon" />
    </router-link>
    <DogBreeds />
  </div>
</template>

<script>
import DogBreeds from "@/components/DogBreeds.vue";

export default {
  name: "Dogs",
  components: {
    DogBreeds,
  },
};
</script>

<style scoped lang="less">
.nav-btn-home {
  margin: 10px;
  width: 50px;
  height: 50px;
}
</style>
