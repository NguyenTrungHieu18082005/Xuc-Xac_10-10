<template>
  <div class="Display">
    <div class="banco"></div>
    <div class="tienThuong">+1.001.123.435</div>

    <div class="vienBanCo">
      <div class="nguoiChoi">
        <div class="nguoiChoi1">
          <p class="soLuong">1023</p>
          <i class="fa-solid fa-users"></i>
        </div>
        <div class="nguoiChoi2">
          <i class="fa-solid fa-users"></i>
          <p class="soLuong">240</p>
        </div>
      </div>

      <div class="vien tai">
        <img class="img" src="/public/assets/tai.png" alt="tai" />
        <p class="tongTienCuoc">tien cuoc</p>
        <button class="cuoc">cuoc</button>
        <p class="tienCuoc">200.000.000</p>
      </div>
      <div class="vien xiu">
        <img class="img" src="/public/assets/xiu.png" alt="tai" />
        <p class="tongTienCuoc">1.723.000.000</p>
        <button class="cuoc">1.000</button>
        <p class="tienCuoc">200.000.000</p>
      </div>
    </div>

    <div class="banTron"></div>
    <div class="tongTien"><p>2.111.222.333</p></div>
    <div class="tongDiem">18</div>
    <div class="thoiGian">60</div>

    <div class="thanhNgang">
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
  props: {
    itemsLi: { type: Array, default: null },
    liIndex: { type: Array, default: null },
    li: { type: Array, default: null },
  },
};
</script>

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
.tongDiem,
.thoiGian,
.nguoiChoi {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  /* background: linear-gradient(to bottom, #2c2ccc, #5fb4ff); */
  background-color: #3fbbec;
}
.tienThuong {
  font-size: 30px;
  font-family: "Anton", sans-serif;
  font-weight: 800;
  top: 70%;
  z-index: 2;
  color: whitesmoke;
  text-shadow: 2px 2px 0px black, -2px -2px 0px black, -2px 2px 0px black,
    2px -2px 0px black;
  letter-spacing: 4px;
  text-align: center;
  background-color: transparent;
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

.nguoiChoi .soLuong {
  padding: 0px 8px;
  font-size: 17px;
  font-weight: 700;
  background-color: #2325b242;
  border-radius: 20px;
  width: 50px;
  height: 15px;
  margin-top: 3px;
}
.banTron {
  width: 180px;
  height: 180px;
  border: 4px double orange;
  border-radius: 50%;
  background-color: black;
}
.tongTien {
  width: 250px;
  /* border: 1px solid #000; */
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
}
.tongDiem {
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
}
.thoiGian {
  background-color: #ffffff73;
  width: 160px;
  height: 160px;
  border: 4px double orange;
  border-radius: 50%;
  text-align: center;
  line-height: 150px;
  font-size: 90px;
  font-weight: bold;
  z-index: 1;
  opacity: 1;
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
}
.vienBanCo .tienCuoc {
  font-weight: 900;
  margin-top: 5px;
}

.Display .thanhNgang {
  position: relative;
  border: 1px solid #000;
  width: 350px;
  height: 18px;
  border-radius: 20px;
  top: 68%;
  left: 50%;
  transform: translateX(-50%);
  background-color: rgb(39, 39, 39);
}
.Display .thanhNgang ul {
  display: flex;
}
.Display .thanhNgang ul li {
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
