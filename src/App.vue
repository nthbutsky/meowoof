<template>
  <div id="nav" v-if="showNav()">
    <p class="nav-text">Choose your folk!</p>
    <router-link to="/cats">
      <img class="nav-btn-pet" src="@/assets/050-cat.svg" alt="Cat Icon" />
    </router-link>
    <router-link class="nav-btn-dog" to="/dogs">
      <img class="nav-btn-pet" src="@/assets/039-dog.svg" alt="Dog Icon" />
    </router-link>
  </div>
  <router-view />
</template>

<script>
export default {
  name: "App",
  data() {
    return;
  },
  methods: {
    showNav() {
      if (this.$route.path === "/") {
        return true;
      } else {
        return false;
      }
    },
  },
};
</script>

<style lang="less">
@import "css/google-fonts.css";
@import "css/css-reset.css";

html,
body {
  height: 100%;
  background: #f0f0f0;
}

#app {
  font-family: "Amatic SC", cursive;
  font-style: normal;
  font-size: 100%;
  text-align: center;
  height: 100%;
}

#nav {
  width: 75%;
  height: 75%;
  margin: 50px auto;
  display: flex;
  justify-content: flex-start;
  flex-direction: column;
}

.nav-text {
  font-size: 3rem;
  font-weight: 700;
  margin: 10px;
  color: #888;
}

.nav-btn-pet {
  max-width: 300px;
  max-height: 300px;
  margin: 10px;
  border-radius: 50%;

  &:hover {
    border-radius: 0;
    width: 305px;
    margin: 10px;
  }
}
</style>
