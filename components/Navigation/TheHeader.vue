<template>
    <div class="header-container">
    <header class="the-header">
    <TheSideNavToggle @toggle="$emit('sidenavToggle')" />
    <div class="logo">
        <nuxt-link 
  tag="img" 
  :src="require('~/assets/logo.png')" 
  to="/">
</nuxt-link>
    </div>
 <div class="spacer"></div>
      <div class="navigation-items">
        <ul class="nav-list">
            <li class="nav-item">
            <nuxt-link to="/">Vremenska prognoza</nuxt-link>
          </li>
          <li class="nav-item">
            <nuxt-link to="/petodnevna">Petodnevna prognoza</nuxt-link>
          </li>
          <li class="nav-item">
            <nuxt-link to="/zanimljivosti">Zanimljivosti</nuxt-link>
          </li>
          <li class="nav-item">
            <nuxt-link to="/onama">O nama</nuxt-link>
          </li>
        </ul>
      </div>
    </header>
  </div>
</template>

<script>
import TheSideNavToggle from "@/components/Navigation/TheSideNavToggle";

export default {
  name: "TheHeader",
  components: {
    TheSideNavToggle
  }
};
</script>


<style scoped>
.header-container {
  height:60px;
}

.the-header {
  width: 100%;
  position: fixed;
  height: 60px;
  display: flex;
  justify-content: space-around;
  align-items: center;
  background-color: blue;
  z-index: 100;
  box-sizing: border-box;
  padding: 0 20px;
}

.spacer {
  flex: 1;
}

.navigation-items {
  display: none;
}

@media (min-width: 768px) {
  .navigation-items {
    display: block;
  }
}

.nav-list {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  font-size: 18px;
  font-family:Arial, Helvetica, sans-serif;
  font-weight: bold;
}

.nav-item {
  margin: 0 100px;
}

.nav-item a {
  text-decoration: none;
  color: white;
}

.nav-item a:hover {
  color: black;
  font-weight: bold;
  font-size:20px;
}
</style>