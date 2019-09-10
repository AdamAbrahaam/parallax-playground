<template>
  <div>
    <div class="layer-black"></div>
    <div class="layer layer-bg"></div>
    <div class="layer layer-text"><h1>Welcome</h1></div>
    <div class="layer layer-one"></div>
    <div class="layer layer-two"></div>
    <div class="layer-button">
      <button id="scrollBtn" @click="$parent.nextPage">Explore!</button>
    </div>
    <div class="layer layer-three"></div>
    <div class="layer-grad"></div>
  </div>
</template>

<script>
export default {
  name: "pMountainMan",
  data() {
    return {
      layers: undefined,
      scrollBtn: undefined
    };
  },

  mounted() {
    this.scrollBtn = document.getElementById("scrollBtn");
    this.layers = document.querySelectorAll(".layer");
  },

  methods: {
    handleScroll() {
      for (let i = 0; i < this.layers.length; i++) {
        this.layers[i].style.transform = "translateY(-" + (window.pageYOffset * i / this.layers.length) + "px)";
      }

      if (window.top.scrollY <= 100) {
        this.scrollBtn.style["opacity"] = 1;
      } else {
        this.scrollBtn.style["opacity"] = 0;
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.layer-bg {
  background-image: url("../assets/parallax/mountainman/layer-bg.png");
}

.layer-one {
  background-image: url("../assets/parallax/mountainman/layer2.png");
}

.layer-two {
  background-image: url("../assets/parallax/mountainman/layer1.png");
}

.layer-three {
  background-image: url("../assets/parallax/mountainman/layer0.png");
}

.layer {
  background-position: bottom;
  background-repeat: no-repeat;
  background-size: cover;
  width: 100%;
  min-height: 100%;
  height: auto;
  position: fixed;
  z-index: -1;
}

.layer-grad {
  width: 100%;
  bottom: 0;
  min-height: 35vh;
  height: auto;
  position: absolute;
  background-image: linear-gradient(to top, black, transparent);
}

.layer-text {
  text-align: center;
  margin-top: 3vh;
  font-size: 130px;
  color: whitesmoke;
}

.layer-black {
  width: 100%;
  min-height: 100vh;
  height: auto;
  position: fixed;
  background-color: black;
  z-index: -1;
}

.layer-button {
  position: absolute;
  width: 100%;
  text-align: center;
  bottom: 0;
  margin-bottom: 5vh;
  z-index: 2;
  opacity: 1;

  button {
    background: transparent;
    transition: opacity 0.9s;
    color: white;
    font-size: 30px;
    outline: 0;

    padding: 10px;
    border: 1px solid white;
    border-radius: 10px 10px;
  }
}
</style>
