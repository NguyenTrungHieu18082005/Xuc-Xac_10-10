<template>
  <div class="Display">
    <div class="banco"></div>

    <div class="vienBanCo">
      <div class="nguoiChoi">
        <div class="nguoiChoi1">
          <p class="soNguoiChoi">{{ SoNguoiChoi[0].s1 }}</p>
          <i class="fa-solid fa-users"></i>
        </div>
        <div class="nguoiChoi2">
          <i class="fa-solid fa-users"></i>
          <p class="soNguoiChoi">{{ SoNguoiChoi[0].s2 }}</p>
        </div>
      </div>

      <div class="vien tai">
        <img class="img" src="/public/assets/tai.png" alt="tai" />
        <p class="tongTienCuoc">{{ xlRandomTongTienCuoc[0] }}</p>
        <button
          class="cuoc Tien1"
          :class="{ on: this.indexTenTienCuoc[0].s1 === 1 }"
          @click="cuoctien1(0)"
        >
          {{ TenTienCuoc[indexTenTienCuoc[0].s1] }}
        </button>
        <p class="tienCuoc">200.000.000</p>
      </div>

      <div class="vien xiu">
        <img class="img" src="/public/assets/xiu.png" alt="tai" />
        <p class="tongTienCuoc">{{ xlRandomTongTienCuoc[1] }}</p>
        <button
          class="cuoc Tien2"
          :class="{ on: this.indexTenTienCuoc[1].s2 === 1 }"
          @click="cuoctien2(1)"
        >
          {{ TenTienCuoc[indexTenTienCuoc[1].s2] }}
        </button>
        <p class="tienCuoc">200.000.000</p>
      </div>
    </div>

    <div class="banTron"></div>

    <div class="xx">
      <div id="dice-1" class="dice">
        <div class="spinner" v-bind:class="'dice-' + Dices[0]">
          <div class="face1">1</div>
          <div class="face2">2</div>
          <div class="face3">3</div>
          <div class="face4">4</div>
          <div class="face5">5</div>
          <div class="face6">6</div>
        </div>
      </div>

      <div id="dice-2" class="dice">
        <div class="spinner" v-bind:class="'dice-' + Dices[1]">
          <div class="face1">1</div>
          <div class="face2">2</div>
          <div class="face3">3</div>
          <div class="face4">4</div>
          <div class="face5">5</div>
          <div class="face6">6</div>
        </div>
      </div>

      <div id="dice-3" class="dice">
        <div class="spinner" v-bind:class="'dice-' + Dices[2]">
          <div class="face1">1</div>
          <div class="face2">2</div>
          <div class="face3">3</div>
          <div class="face4">4</div>
          <div class="face5">5</div>
          <div class="face6">6</div>
        </div>
      </div>
    </div>

    <div class="thoiGian" :class="{ on: this.TatHienThiThoiGian }">
      {{ ThoiGian }}
    </div>
    <div class="tienThuong">+1.001.123.435</div>
    <div class="tongTien">
      <p :class="{ on: this.HienThiTongTien === true }">
        {{ xlRandomTongTien[0] }}
      </p>
    </div>
    <div class="thoiGianVanMoi" :class="{ on: this.HienThiThoiGianVanMoi }">
      {{ ThoiGianVanMoi }}
    </div>

    <div class="thanhNgang" :class="{ Stop: this.BatDau }">
      <ul>
        <li
          v-for="(i, id) in itemsLi"
          :key="id"
          :class="{ active: liIndex.includes(id + 1) }"
        ></li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "Display",
  data() {
    return {
      TenTienCuoc: ["Cược", "0"],
      indexTenTienCuoc: [{ s1: 0 }, { s2: 0 }],
    };
  },
  props: {
    xlRandomTongTienCuoc: { typeof: Array, default: [0, 0] },
    SoNguoiChoi: { type: Array, default: [0] },
    xlRandomTongTien: { type: Array, default: null },
    HienThiTongTien: { type: Boolean, default: false },
    HienThiThoiGianVanMoi: { type: Boolean, default: false },
    ThoiGianVanMoi: { type: Number, default: 10 },
    TatHienThiThoiGian: { type: Boolean, default: false },
    ThoiGian: { type: Number, default: 45 },
    itemsLi: { type: Array, default: null },
    liIndex: { type: Array, default: null },
    BatDau: { type: Boolean, default: false },
    Dices: { type: Array, default: [1, 2, 3] },
  },
  methods: {
    cuoctien1(e) {
      this.$emit("xlCuocTien", e);
      this.indexTenTienCuoc[0].s1 = this.indexTenTienCuoc[0].s1 === 0 ? 1 : 0;
    },
    cuoctien2(e) {
      this.$emit("xlCuocTien", e);
      this.indexTenTienCuoc[1].s2 = this.indexTenTienCuoc[1].s2 === 0 ? 1 : 0;
    },
  },
};
</script>
''
<style>
:root {
  --mauBanCo: #0e9ff3;
}
.Display {
  /* background-color: #09e7d168; */
  width: 700px;
  height: 400px;
  position: relative;
}
.tienThuong,
.banco,
.vienBanCo,
.banTron,
.tongTien,
.thoiGianVanMoi,
.thoiGian,
.nguoiChoi {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: #3fbbec;
}

.banco {
  width: 650px;
  height: 300px;
  border: 1px solid black;
  border-radius: 130px;
  background-color: var(--mauBanCo);
}

.vienBanCo {
  width: 590px;
  height: 240px;
  border: 1px solid white;
  border-radius: 110px;

  display: flex;
  justify-content: space-around;
  align-items: center;
}
.nguoiChoi {
  /* border: 1px solid #000; */
  width: 250px;
  height: 20px;
  top: 10%;
  display: flex;
  justify-content: space-between;
}
.nguoiChoi .nguoiChoi1,
.nguoiChoi .nguoiChoi2 {
  display: flex;
}

.nguoiChoi .soNguoiChoi {
  padding: 0px 8px;
  font-size: 17px;
  font-weight: 700;
  background-color: #2325b242;
  border-radius: 20px;
  width: 50px;
  height: 15px;
  margin-top: 3px;
}

.vienBanCo .vien.tai,
.vienBanCo .vien.xiu {
  width: 130px;
  height: 180px;
  /* border: 1px solid #0b9b45; */
  border-radius: 10px;
  margin-top: 30px;
}
.vienBanCo .vien {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}
.vienBanCo .tai {
  margin-left: -70px;
}
.vienBanCo .xiu {
  margin-right: -70px;
}

.vienBanCo .img {
  width: 100px;
  height: 55px;
  border: none;
  margin-top: -10px;
  border-radius: 15px;
}

.vienBanCo .tongTienCuoc {
  /* border: 1px solid #000; */
  margin-top: 7px;
  text-align: center;
  color: orangered;
  font-size: 23px;
  font-family: "Anton", sans-serif;
  font-weight: 500;
}
.cuoc {
  width: 100px;
  height: 30px;
  border-radius: 15px;
  font-size: 15px;
  font-family: "Anton", sans-serif;
  font-weight: 500;
  color: white;
  background: orange;
  border: 1px solid white;
  margin: 7px 0;
  cursor: pointer;
}
.cuoc.Tien1.on,
.cuoc.Tien2.on {
  background: #000;
}

.tienCuoc {
  font-weight: 900;
  margin-top: 5px;
}

.banTron {
  width: 180px;
  height: 180px;
  border: 5px double orange;
  border-radius: 50%;
  background-color: black;
}

.xx {
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 180px;
  height: 180px;
  background-color: transparent;
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

.thoiGian {
  background-color: #726b6b;
  width: 160px;
  height: 160px;
  border: 4px double orange;
  border-radius: 50%;
  text-align: center;
  line-height: 150px;
  font-size: 90px;
  font-weight: bold;
  opacity: 1;
}
.thoiGian.on {
  opacity: 0;
  visibility: hidden;
}
.tienThuong {
  font-size: 30px;
  font-family: "Anton", sans-serif;
  font-weight: 800;
  top: 70%;
  color: whitesmoke;
  text-shadow: 2px 2px 0px black, -2px -2px 0px black, -2px 2px 0px black,
    2px -2px 0px black;
  letter-spacing: 4px;
  text-align: center;
  background-color: transparent;
  /* visibility: hidden; */
}

.tongTien {
  width: 250px;
  position: relative;
  top: 17%;

  border-top: 40px solid rgba(1, 85, 255, 0.623);
  border-bottom: 0px;
  border-left: 30px solid var(--mauBanCo); /* Làm trong suốt viền bên trái */
  border-right: 30px solid var(--mauBanCo); /* Làm trong suốt viền bên phải */

  border-bottom-left-radius: 50px;
  border-bottom-right-radius: 50px;
}
.tongTien p {
  position: absolute;
  left: 50%;
  margin-top: -20%;
  transform: translate(-50%, 0);
  font-size: 29px;
  font-family: "Anton", sans-serif;
  font-weight: 800;
  letter-spacing: 2px;
  background: linear-gradient(to bottom, gold, rgb(51, 255, 0));
  background-clip: text;
  color: transparent;

  visibility: hidden;
}
.tongTien p.on {
  visibility: visible;
}

.thoiGianVanMoi {
  width: 35px;
  height: 35px;
  border: 1px solid #313131;
  border-radius: 50%;
  top: 28%;
  background-color: rgba(75, 74, 74, 0.827);
  text-align: center;
  line-height: 25px;
  font-size: 25px;
  font-weight: bold;
  color: whitesmoke;

  opacity: 0;
  visibility: hidden;
}
.thoiGianVanMoi.on {
  opacity: 1;
  visibility: visible;
}

.thanhNgang {
  position: relative;
  border: 1px solid #000;
  width: 350px;
  height: 18px;
  border-radius: 20px;
  top: 68%;
  left: 50%;
  transform: translateX(-50%);
  background-color: rgb(39, 39, 39);
  visibility: hidden;
}
.thanhNgang.Stop {
  visibility: visible;
}
.thanhNgang ul {
  display: flex;
}
.thanhNgang ul li {
  width: 13px;
  height: 11px;
  border: 1px solid rgba(255, 255, 255, 0.336);
  border-radius: 50%;
  margin: 2px;
  list-style-type: none;
  background-color: black;
}

.thanhNgang ul li.active {
  background-color: #fff;
}
</style>
