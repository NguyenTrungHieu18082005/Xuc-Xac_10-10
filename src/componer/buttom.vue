<template>
  <div class="Button">
    <div class="menuTienCuoc">
      <ul>
        <li class="liDatCuoc" v-for="(i, id) in datcuoc" :key="id">
          <button>{{ i }}</button>
        </li>
      </ul>
    </div>

    <div class="chucnangButton">
      <button class="button-blue">TẤT CẢ</button>
      <button class="button-gold">ĐẶT CƯỢC</button>
      <button class="button-red">HỦY</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Button",
  props: {
    datcuoc: { type: String, default: null },
  },
};
</script>

<style>
.Button {
  top: 57%;
  left: 7%;
  transform: translateY(-57%);
  /* background-color: #489a1868; */
  width: 600px;
  height: 30px;
  position: absolute;
  /* opacity: 0; */
  /* visibility: hidden; */
}
.menuTienCuoc {
  width: 600px;
  height: 30px;

  /* left: 50%; */
  left: 260px;
  transform: translateX(-50%);
  /* background-color: #e20fbc; */
  /* border: 1px solid #000; */
  position: absolute;
}

.menuTienCuoc ul {
  display: flex;
  justify-content: space-between;
}
.menuTienCuoc ul li {
  list-style-type: none;
}
.menuTienCuoc ul li button {
  width: 75px;
  height: 30px;
  border-radius: 11px;
  background: linear-gradient(to bottom, #0000ff, #87ceeb);
  border: 1px solid orange;
  font-weight: 800;
  cursor: pointer;
  color: yellow;
}
.menuTienCuoc ul li button:hover {
  background: rgb(37, 37, 186);
}

.Button .chucnangButton {
  position: absolute;
  /* width: 500px;
  height: 50px; */
  /* background-color: #c50a0a; */

  top: 120%;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  /* justify-content: space-evenly;ss */
}
.chucnangButton button {
  color: white;
  font-weight: 600;
  font-size: 17px;
  cursor: pointer;
}
.chucnangButton button:hover {
  background: rgb(37, 37, 186);
}
.button-blue {
  transform: skew(35deg);
  border-bottom-left-radius: 20px;
  width: 150px;
  height: 40px;
  background-color: #0e1f44;
}
.button-gold {
  width: 200px;
  height: 45px;
  background-color: hsl(234, 55%, 29%); /* Màu sắc của hình thang */
  clip-path: polygon(0% 0%, 100% 0%, 85% 100%, 15% 100%);
  border: none;
}
.button-red {
  transform: skew(-35deg);
  border-bottom-right-radius: 20px;
  width: 150px;
  background-color: #0e1f44;
  height: 40px;
}
</style>
