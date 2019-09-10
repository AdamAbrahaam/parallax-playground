<template>
  <div id="app">
    <section class="header page" id="home">
      <component v-bind:is="currentParallax" ref="childComponent" v-cloak />
    </section>

    <div class="mobile">
      <h1>
        Mobile version in progress,<br />
        visit on PC for a stunning experience!
      </h1>
    </div>

    <section id="content">
      <div class="content-container page">
        <Accordion id="compAccordion" />
      </div>
    </section>
  </div>
</template>

<script>
import VueScrollTo from "vue-scrollto";
import Accordion from "./components/Accordion.vue";
import pMountainMan from "./components/pMountainMan.vue";
import pFoxIllustration from "./components/pFoxIllustration.vue";
import pPilot from "./components/pPilot.vue";
import pDesert from "./components/pDesert.vue";

export default {
  name: "app",
  components: {
    Accordion,
    pMountainMan,
    pFoxIllustration,
    pPilot,
    pDesert
  },

  data() {
    return {
      active: "p-mountain-man",
      parallaxes: [
        "p-mountain-man",
        "p-fox-illustration",
        "p-pilot",
        "p-desert"
      ],
      scrollSpeed: 2000,
      layers: undefined,
      scrollBtn: undefined,
      canScroll: true,
      sections: undefined,
      currentSection: undefined,
      compAccordion: undefined
    };
  },

  computed: {
    currentParallax: function() {
      return this.active;
    }
  },

  methods: {
    changeParallax(id) {
      this.active = this.parallaxes[id];
      this.compAccordion.style.pointerEvents = "none";
      this.canScroll = false;
      setTimeout(() => this.previousPage(), 1000);
    },

    handleScroll() {
      this.$refs.childComponent.handleScroll();
    },

    handleWheel(e) {
      if (e.deltaY < 0 && this.canScroll) {
        this.canScroll = false;
        this.previousPage();
      } else if (e.deltaY > 0 && this.canScroll) {
        this.canScroll = false;
        this.nextPage();
      }
    },

    nextPage() {
      let nextPage = this.sections[++this.currentSection];
      if (nextPage !== undefined) {
        let vm = this;
        VueScrollTo.scrollTo(nextPage, this.scrollSpeed, {
          easing: "ease-out",
          cancelable: false,
          onDone: function() {
            vm.canScroll = true;
            vm.compAccordion.style.pointerEvents = "all";
          }
        });
      } else {
        --this.currentSection;
        this.canScroll = true;
      }
    },

    previousPage() {
      let previousPage = this.sections[--this.currentSection];
      if (previousPage !== undefined) {
        let vm = this;
        VueScrollTo.scrollTo(previousPage, this.scrollSpeed, {
          easing: "ease-out",
          cancelable: false,
          onDone: function() {
            vm.canScroll = true;
          }
        });
      } else {
        ++this.currentSection;
        this.canScroll = true;
      }
    }
  },

  mounted() {
    this.scrollBtn = document.getElementById("scrollBtn");
    this.compAccordion = document.getElementById("compAccordion");
    this.layers = document.querySelectorAll(".layer");
    this.sections = document.querySelectorAll(".page");
    this.currentSection = 0;

    window.addEventListener("scroll", this.handleScroll);
    window.addEventListener("wheel", this.handleWheel);
  },
  beforeDestroy() {
    window.removeEventListener("scroll", this.handleScroll);
  }
};
</script>

<style lang="scss">
[v-cloak] > * {
  display: none;
}
[v-cloak]::before {
  content: "loading…";
  color: black;
}

:root {
  overflow: hidden;
}

body,
h1,
h2,
ul {
  margin: 0;
  padding: 0;
}

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.loading {
  position: fixed;
  background: transparent;
  opacity: 0.96;
  width: 100vw;
  height: 100vh;
  text-align: center;
  z-index: 3;
  margin: 0 auto;

  h1 {
    color: white;
    font-size: 50px;
  }
}

.header {
  scroll-behavior: smooth;
  min-height: 100vh; /*Background height*/
  height: auto;
  overflow: hidden;
  position: relative;
}

#content {
  min-height: 200vh;
  padding-top: 5vh;
  background-color: black;
}

.content-container {
  color: white;
  margin: 0 auto;
  min-height: 100vh;

  #compAccordion {
    pointer-events: none;
  }
}

.mobile {
  display: none;
  min-height: 100vh;
  min-width: 100vw;
  background: #252525;

  h1 {
    font-size: 20px;
    padding-top: 50%;
    color: #00ff00d4;
    text-align: center;
  }
}

@media (max-width: 768px) {
  #home,
  #content {
    display: none;
  }

  .mobile {
    display: block;
  }
}
</style>
