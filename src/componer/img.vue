<template>
  <div class="dices1">
    <div class="xx">
      <div id="dice-1" class="dice">
        <div class="spinner" v-bind:class="'dice-' + dices[0]">
          <div class="face1">1</div>
          <div class="face2">2</div>
          <div class="face3">3</div>
          <div class="face4">4</div>
          <div class="face5">5</div>
          <div class="face6">6</div>
        </div>
      </div>

      <div id="dice-2" class="dice">
        <div class="spinner" v-bind:class="'dice-' + dices[1]">
          <div class="face1">1</div>
          <div class="face2">2</div>
          <div class="face3">3</div>
          <div class="face4">4</div>
          <div class="face5">5</div>
          <div class="face6">6</div>
        </div>
      </div>

      <div id="dice-3" class="dice">
        <div class="spinner" v-bind:class="'dice-' + dices[2]">
          <div class="face1">1</div>
          <div class="face2">2</div>
          <div class="face3">3</div>
          <div class="face4">4</div>
          <div class="face5">5</div>
          <div class="face6">6</div>
        </div>
      </div>
    </div>

    <button class="bt" @click="click1">click</button>
  </div>
</template>

<script>
export default {
  name: "dices1",
  props: {
    dices: { type: Array, default: [2, 2, 2] },
  },
  methods: {
    click1() {
      this.$emit("randon");
    },
  },
};
</script>

<style>
.dices1 {
  top: 30%;
  left: 311px;
  transform: translate(-30%, -41%);
  width: 180px;
  height: 180px;
  /* background-color: #1818be23; */
  position: absolute;
  border-radius: 50%;

  /* visibility: hidden; */
}

.xx {
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 180px;
  height: 180px;
  /* border-radius: 50%; */
  /* border: 1px solid #8adb09; */
  /* background-color: black; */
  position: absolute;

  display: grid;
  grid-template-areas:
    "h t"
    "f f";
}

.dice {
  /* background-color: #fff; */
  width: 50px;
  height: 50px;
  /* border: 1px solid #000; */
  margin-top: 50px;
  margin-left: 15px;
  transform: rotate(45deg);
  /* margin-top: 50px;
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  width: 60px;
  height: 60px;
  box-shadow: 0px 10px 60px rgba(0, 0, 0, 0.1);
  border: 1px solid #000;
  background-color: #d6cbcb37; */
}
#dice-1 {
  grid-area: h;
  margin-left: 29px;
}
#dice-2 {
  grid-area: t;
  margin-right: 19px;
}
#dice-3 {
  grid-area: f;
  margin-left: 66px;
  margin-top: -50px;
}

.spinner div {
  position: absolute;
  width: 50px;
  height: 50px;
  border: 1px solid #ccc;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.2);
  text-align: center;
  line-height: 120px;
  font-size: 100px;
  color: #ff00e1;
  font-size: 0px;
  transition: all 0.1s ease;
  opacity: 1;
}

.bt {
  top: 100%;
  left: 133%;
  position: absolute;
  width: 70px;
  border: none;
  cursor: pointer;
}
.spinner .face1 {
  -webkit-transform: translateZ(60px);
  -ms-transform: translateZ(60px);
  transform: translateZ(25px);
  background-image: url("/src/assets/1.png");
  background-position: center;
  background-size: cover;
}
.spinner .face2 {
  -webkit-transform: rotateY(90deg) translateZ(60px);
  -ms-transform: rotateY(90deg) translateZ(60px);
  transform: rotateY(90deg) translateZ(25px);
  background-image: url("/src/assets/2.png");
  background-position: center;
  background-size: cover;
}
.spinner .face3 {
  -webkit-transform: rotateY(90deg) rotateX(90deg) translateZ(60px);
  -ms-transform: rotateY(90deg) rotateX(90deg) translateZ(60px);
  transform: rotateY(90deg) rotateX(90deg) translateZ(25px);
  background-image: url("/src/assets/3.png");
  background-position: center;
  background-size: cover;
}
.spinner .face4 {
  -webkit-transform: rotateY(180deg) rotateZ(90deg) translateZ(60px);
  -ms-transform: rotateY(180deg) rotateZ(90deg) translateZ(60px);
  transform: rotateY(180deg) rotateZ(90deg) translateZ(25px);
  background-image: url("/src/assets/4.png");
  background-position: center;
  background-size: cover;
}
.spinner .face5 {
  -webkit-transform: rotateY(-90deg) rotateZ(90deg) translateZ(60px);
  -ms-transform: rotateY(-90deg) rotateZ(90deg) translateZ(60px);
  transform: rotateY(-90deg) rotateZ(90deg) translateZ(25px);
  background-image: url("/src/assets/5.png");
  background-position: center;
  background-size: cover;
}
.spinner .face6 {
  -webkit-transform: rotateX(-90deg) translateZ(60px);
  -ms-transform: rotateX(-90deg) translateZ(60px);
  transform: rotateX(-90deg) translateZ(25px);
  background-image: url("/src/assets/6.png");
  background-position: center;
  background-size: cover;
}

.spinner {
  -webkit-transform-style: preserve-3d;
  -ms-transform-style: preserve-3d;
  transform-style: preserve-3d;
  -webkit-transform-origin: 60px 60px 0;
  -ms-transform-origin: 60px 60px 0;
  transform-origin: 25px 25px 0;
  -webkit-transition: all 0.5s ease;
  -o-transition: all 0.5s ease;
  transition: all 0.5s ease;
  -webkit-transform: rotateX(0deg) rotateY(0deg) rotateZ(0deg);
  -ms-transform: rotateX(0deg) rotateY(0deg) rotateZ(0deg);
  -o-transform: rotateX(0deg) rotateY(0deg) rotateZ(0deg);
  transform: rotateX(0deg) rotateY(0deg) rotateZ(0deg);
}

.spinner.dice-1 {
  -webkit-transform: rotateX(0deg) rotateY(0deg) rotateZ(0deg);
  -ms-transform: rotateX(0deg) rotateY(0deg) rotateZ(0deg);
  -o-transform: rotateX(0deg) rotateY(0deg) rotateZ(0deg);
  transform: rotateX(0deg) rotateY(0deg) rotateZ(0deg);
}
.spinner.dice-2 {
  -webkit-transform: rotateX(0deg) rotateY(-90deg) rotateZ(0deg);
  -ms-transform: rotateX(0deg) rotateY(-90deg) rotateZ(0deg);
  -o-transform: rotateX(0deg) rotateY(-90deg) rotateZ(0deg);
  transform: rotateX(0deg) rotateY(-90deg) rotateZ(0deg);
}
.spinner.dice-3 {
  -webkit-transform: rotateX(0deg) rotateY(-90deg) rotateZ(90deg);
  -ms-transform: rotateX(0deg) rotateY(-90deg) rotateZ(90deg);
  -o-transform: rotateX(0deg) rotateY(-90deg) rotateZ(90deg);
  transform: rotateX(0deg) rotateY(-90deg) rotateZ(90deg);
}
.spinner.dice-4 {
  -webkit-transform: rotateX(0deg) rotateY(180deg) rotateZ(90deg);
  -ms-transform: rotateX(0deg) rotateY(180deg) rotateZ(90deg);
  -o-transform: rotateX(0deg) rotateY(180deg) rotateZ(90deg);
  transform: rotateX(0deg) rotateY(180deg) rotateZ(90deg);
}
.spinner.dice-5 {
  -webkit-transform: rotateX(0deg) rotateY(90deg) rotateZ(0deg);
  -ms-transform: rotateX(0deg) rotateY(90deg) rotateZ(0deg);
  -o-transform: rotateX(0deg) rotateY(90deg) rotateZ(0deg);
  transform: rotateX(0deg) rotateY(90deg) rotateZ(0deg);
}
.spinner.dice-6 {
  -webkit-transform: rotateX(90deg) rotateY(90deg) rotateZ(0deg);
  -ms-transform: rotateX(90deg) rotateY(90deg) rotateZ(0deg);
  -o-transform: rotateX(90deg) rotateY(90deg) rotateZ(0deg);
  transform: rotateX(90deg) rotateY(90deg) rotateZ(0deg);
}
</style>
