<template>
  <div class="accordion">
    <ul>
      <li @click="active = 0" :class="{ active: active == 0 }">
        <div class="section-title">
          <button class="close-btn" @click.stop="active = undefined">X</button>
          <h2>Mountains</h2>
        </div>
        <div class="section-content">
          <button @click="$parent.changeParallax(active)">change !</button>
        </div>
      </li>
      <li @click="active = 1" :class="{ active: active == 1 }">
        <div class="section-title">
          <button class="close-btn" @click.stop="active = undefined">X</button>
          <h2>Fox Illustration</h2>
        </div>
        <div class="section-content">
          <button @click="$parent.changeParallax(active)">change !</button>
        </div>
      </li>
      <li @click="active = 2" :class="{ active: active == 2 }">
        <div class="section-title">
          <button class="close-btn" @click.stop="active = undefined">X</button>
          <h2>Pilot</h2>
        </div>
        <div class="section-content">
          <button @click="$parent.changeParallax(active)">change !</button>
        </div>
      </li>
      <li @click="active = 3" :class="{ active: active == 3 }">
        <div class="section-title">
          <button class="close-btn" @click.stop="active = undefined">X</button>
          <h2>Desert</h2>
        </div>
        <div class="section-content">
          <button @click="$parent.changeParallax(active)">change !</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Accordion",

  data: () => ({
    active: undefined
  })
};
</script>

<style scoped lang="scss">
* {
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}

.accordion {
  position: absolute;
  height: 100%;
  width: 100%;
  padding: 15vh;
}

li:nth-child(1) {
  background-image: url("../assets/parallax/mountainman/original.jpg");
}
li:nth-child(2) {
  background-image: url("../assets/parallax/foxillustration/original.png");
}
li:nth-child(3) {
  background-image: url("../assets/parallax/pilot/original.jpg");
}
li:nth-child(4) {
  background-image: url("../assets/parallax/desert/original.jpg");
}

ul {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  height: 100%;
  list-style-type: none;
  -webkit-box-shadow: 0px 0px 80px 0px rgba(255, 255, 255, 0.75);
  box-shadow: 0px 0px 80px 0px rgba(255, 255, 255, 0.75);
}

li {
  background-size: cover;
  background-position: center;
  -webkit-box-flex: 1;
  -ms-flex: 1;
  flex: 1;
  -ms-flex-item-align: center;
  align-self: center;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  height: 100%;
  padding: 20px;
  cursor: pointer;
  -webkit-transition: all 0.5s ease;
  -o-transition: all 0.5s ease;
  transition: all 0.5s ease;
  -webkit-box-shadow: inset 0 0 0 1000px rgba(25, 25, 60, 0.5);
  box-shadow: inset 0 0 0 1000px rgba(25, 25, 60, 0.5);

  &:hover {
    -webkit-box-flex: 1.1;
    -ms-flex: 1.1;
    flex: 1.1;
    -webkit-box-shadow: none;
    box-shadow: none;
  }

  &.active {
    -webkit-box-flex: 5;
    -ms-flex: 5;
    flex: 5;
    -webkit-box-shadow: none;
    box-shadow: none;
    cursor: default;

    .section-content {
      opacity: 1;
      color: #e74c3c;
    }

    .close-btn {
      opacity: 1;
    }
  }
}

.section-title {
  -webkit-box-flex: 1;
  -ms-flex: 1;
  flex: 1;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-ordinal-group: 2;
  -ms-flex-order: 1;
  order: 1;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -ms-flex-direction: column;
  flex-direction: column;
  -webkit-box-pack: justify;
  -ms-flex-pack: justify;
  justify-content: space-between;
  -webkit-box-align: end;
  -ms-flex-align: end;
  align-items: flex-end;
  color: white;
  max-width: -webkit-fit-content;
  max-width: -moz-fit-content;
  max-width: fit-content;

  h2 {
    -webkit-writing-mode: vertical-rl;
    -ms-writing-mode: tb-rl;
    writing-mode: vertical-rl;
    -webkit-transform: rotate(180deg);
    -ms-transform: rotate(180deg);
    transform: rotate(180deg);
    white-space: nowrap;
  }

  .close-btn {
    opacity: 0;
    -ms-flex-item-align: end;
    align-self: flex-end;
  }
}

.section-content {
  -webkit-box-flex: 1;
  -ms-flex: 1;
  flex: 1;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  margin: 0;
  padding: 0;
  opacity: 0;
  -webkit-transition: all 0.25s 0.1s ease-out;
  -o-transition: all 0.25s 0.1s ease-out;
  transition: all 0.25s 0.1s ease-out;

  button {
    background: rgba($color: #000000, $alpha: 0.2);
    margin: auto auto;
    font-size: 30px;
    color: white;
    padding: 5px;
    border: 1px solid transparent;
    outline: 0;
    border-radius: 10px 10px;
    transition: all 0.5s;
  }

  button:hover {
    font-size: 50px;
  }
}
</style>
