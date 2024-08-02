<template>
  <div class="Funcition">
    <div class="batDau Stop">Chọn Bắt Đầu Để Chơi</div>
    <div class="thanh thanh1">
      <div class="choi">
        <i class="fa-sharp-duotone fa-solid fa-circle-play" title="Bắt Đầu"></i>
      </div>
      <div class="admin">
        <i class="fa-sharp-duotone fa-solid fa-user-gear" title="Admin"></i>
      </div>
    </div>
    <div class="thanh thanh2">
      <div class="luatChoi">
        <i class="fa-sharp fa-solid fa-info" title="Luật Chơi"></i>
      </div>
      <div class="nap">
        <i
          class="fa-sharp-duotone fa-solid fa-money-bill-transfer"
          title="Nạp Tiền"
        ></i>
      </div>
    </div>
    <div class="thanh thanh3">
      <div class="choiLai">
        <i class="fa-sharp-duotone fa-solid fa-rotate" title="Chơi Lại"></i>
      </div>
      <div class="rutTien">
        <i
          class="fa-sharp fa-solid fa-hand-holding-dollar"
          title="Rút Tiền"
        ></i>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Funcition",
};
</script>

<style>
.Funcition {
  left: 1%;
  top: 16%;
  position: absolute;
  width: 680px;
  height: 200px;
  /* border: 1px solid black; */
  border-radius: 130px;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}
.batDau {
  width: 580px;
  height: 210px;
  border-radius: 110px;

  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: #3fbbec;
  z-index: 3;
  text-align: center;
  font-size: 50px;
  font-weight: bold;
  padding-top: 50px;
}
.batDau .Stop {
  visibility: hidden;
}
.Funcition .thanh {
  width: 670px;
  height: 40px;
  /* border: 1px solid #d807b8; */
  display: flex;
  justify-content: space-between;
}
.thanh div {
  width: 40px;
  height: 40px;
  border: 1px solid rgba(255, 255, 255, 0.831);
  border-radius: 50%;
  cursor: pointer;
  color: whitesmoke;
  display: flex;
  justify-content: center;
  align-items: center;
  background: linear-gradient(to bottom, #2525ffe6, #58a6eb);
}
.thanh div:hover {
  background: rgb(37, 37, 186);
}
.thanh div i {
  font-size: 20px;
}

.Funcition .thanh1,
.Funcition .thanh3 {
  width: 655px;
  margin-left: 15px;
}
.Funcition .thanh2 {
  width: 685px;
}
</style>
