<template>
  <div id="app">
    <display :itemsLi="itemsLi" :liIndex="liIndex" :li="li" />
    <image-component :dices="dices" @randon="randon" />
    <buttom :datcuoc="datcuoc" />
    <funcition />
  </div>
</template>

<script>
import ImageComponent from "./componer/img.vue";
import Display from "./componer/display.vue";
import Buttom from "./componer/buttom.vue";
import Funcition from "./componer/funcition.vue";
export default {
  name: "App",
  data() {
    return {
      dices: [3, 4, 6],
      datcuoc: ["1K", "10K", "50K", "100K", "500K", "1M", "10M", "50M"],
      itemsLi: Array(20).fill(""),
      liIndex: [3, 4, 6, 7, 11, 13, 14, 15, 19],
    };
  },
  components: {
    ImageComponent,
    Display,
    Buttom,
    Funcition,
  },
  methods: {
    randon() {
      let count = 0,
        dices1 = 0,
        dices2 = 0,
        dices3 = 0;
      let t = setInterval(() => {
        if (count < 10) {
          dices1 = Math.floor(Math.random() * 6) + 1;
          dices2 = Math.floor(Math.random() * 6) + 1;
          dices3 = Math.floor(Math.random() * 6) + 1;
        } else if (count >= 10) {
          dices1 = Math.floor(Math.random() * 2) + 1;
          dices2 = Math.floor(Math.random() * 2) + 1;
          dices3 = Math.floor(Math.random() * 2) + 1;
        }

        this.dices = [dices1, dices2, dices3];
        console.log(this.dices, count++);
        // if (this.dices[0] === 1 && this.dices[1] === 2 && this.dices[2] === 1) {
        //   clearInterval(t);
        // }
        if (count === 10) {
          clearInterval(t);
        }
      }, 500);
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  width: 1000px;
  /* background-color: #957171; */
  /* margin: 0 auto; */
}
</style>
