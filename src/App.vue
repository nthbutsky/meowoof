<template>
  <div id="nav" v-if="showNav()">
    <div class="nav-text">
      <p>Choose your folk!</p>
    </div>
    <div class="nav__container">
      <router-link to="/cats">
        <img class="nav-btn-pet" src="@/assets/050-cat.svg" alt="Cat Icon" />
      </router-link>
      <router-link class="nav-btn-dog" to="/dogs">
        <img class="nav-btn-pet" src="@/assets/039-dog.svg" alt="Dog Icon" />
      </router-link>
    </div>
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

#app {
  font-family: "Amatic SC", cursive;
  font-style: normal;
  font-size: 100%;
  text-align: center;
  padding-top: 1.875rem;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  align-content: center;
  flex-direction: column;
  flex-wrap: nowrap;
}
body {
  background: #f0f0f0;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: black;

    &.router-link-exact-active {
      color: #ff868e;

      &:active {
        background: #ff868e;
        color: white;
      }
    }
  }
}

.nav__container {
  display: flex;
  justify-content: center;
  flex-direction: row;
  align-content: center;
  flex-wrap: wrap;
  align-items: center;
}

.nav-text {
  font-size: 50px;
  font-weight: 700;
  padding: 20px;
  margin: 10px;
  color: #888;
}

.nav-btn-pet {
  width: 300px;
  margin: 10px;
  border-radius: 50%;
  @media (max-width: 400px) {
    width: 200px;
  }

  &:hover {
    border-radius: 0;
    width: 305px;
    margin: 7.5px;
    @media (max-width: 400px) {
      width: 205px;
    }
  }
}
</style>
