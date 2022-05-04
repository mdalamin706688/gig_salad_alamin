<template>
  <v-app>
    <Navigation :color="color" :flat="flat" />
    <v-main class="pt-0">
      <Home />
      <About />
      <Download />
      <Pricing />
      <Contact />
    </v-main>
    <v-scale-transition>
      <v-btn
        fab
        v-show="fab"
        v-scroll="onScroll"
        dark
        fixed
        bottom
        right
        color="secondary"
        @click="toTop"
      >
        <v-icon>mdi-arrow-up</v-icon>
      </v-btn>
    </v-scale-transition>
    <Footer />
  </v-app>
</template>

<style scoped>
.v-main {
  background-image: url("~@/assets/img/bgMain.png");
  background-attachment: fixed;
  background-position: center;
  background-size: cover;
}
</style>

<script>
import Navigation from "./components/navigation";
import Footer from "./components/footer";
import Home from "./components/homeSection";
import About from "./components/aboutSection";
import Download from "./components/downloadSection";
import Pricing from "./components/pricingSection";
import Contact from "./components/contactSection";

export default {
  name: "App",

  components: {
    Navigation,
    Footer,
    Home,
    About,
    Download,
    Pricing,
    Contact,
  },

  data: () => ({
    fab: null,
    color: "",
    flat: null,
  }),

  created() {
    const top = window.pageYOffset || 0;
    if (top <= 60) {
      this.color = "transparent";
      this.flat = true;
    }
  },

  watch: {
    fab(value) {
      if (value) {
        this.color = "secondary";
        this.flat = false;
      } else {
        this.color = "transparent";
        this.flat = true;
      }
    },
  },

  methods: {
    onScroll(e) {
      if (typeof window === "undefined") return;
      const top = window.pageYOffset || e.target.scrollTop || 0;
      this.fab = top > 60;
    },
    toTop() {
      this.$vuetify.goTo(0);
    },
  },
};
</script>
