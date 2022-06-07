<template>
  <div class="app-container">
    <TheHeader @sidenavToggle="displaySidenav = !displaySidenav" />

    <TheSideNav :show="displaySidenav" @close="displaySidenav = false" />
    <div class="app-content">
      <nuxt />
    </div> 
    <TheFooter />
    </div>
</template>

<script>
import TheHeader from "@/components/Navigation/TheHeader";
import TheSidenav from "@/components/Navigation/TheSidenav";
import TheFooter from "@/components/Navigation/TheFooter";

export default {
  components: {
    TheHeader,
    TheSidenav,
    TheFooter
  },
  data() {
    return {
      displaySidenav: false
    };
  }
};
</script>>

<style>
html {
  font-size: 13pt;
}
@media screen and (max-width: 1680px) {
  html {
    font-size: 11pt;
  }
}
@media screen and (max-width: 980px) {
  html {
    font-size: 12pt;
  }
}
@media screen and (max-width: 480px) {
  html {
    font-size: 11pt;
  }
}

div {
  border-radius: 5px;
}

body {
  background-color: #ffffff;
  color: #444444;
}

body {
  font-weight: 400;
  font-size: 1rem;
  line-height: 1.65;
  box-sizing: border-box;
  color: #201e1e;
  font-family: "Manrope", sans-serif;
}

body {
  margin: 0;
}
</style>
