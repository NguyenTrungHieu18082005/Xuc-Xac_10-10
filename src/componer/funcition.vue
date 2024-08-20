<template>
  <div class="Funcition">
    <div class="batDauChoi" :class="{ Stop: this.BatDau }">
      Chọn Bắt Đầu Để Chơi
    </div>

    <div class="t thanh1">
      <i
        class="fa-sharp-duotone fa-solid fa-circle-play batDau"
        title="Bắt Đầu"
        @click="batdau"
        :class="{ disabledBatDau: this.BatDau }"
      ></i>
      <i
        class="fa-sharp fa-solid fa-info luatChoi"
        title="Luật Chơi"
        @click="luatchoi"
      ></i>
      <i
        class="fa-sharp-duotone fa-solid fa-rotate choiLai"
        title="Chơi Lại"
        @click="choilai"
        :class="{ on: this.BatDau }"
      ></i>
    </div>

    <div class="t thanh2">
      <i
        class="fa-sharp-duotone fa-solid fa-user-gear admin"
        title="Admin"
        @click="admin"
      ></i>
      <i
        class="fa-sharp-duotone fa-solid fa-money-bill-transfer napTien"
        title="Nạp Tiền"
        @click="naptien"
        :class="{ on: this.BatDau }"
      ></i>
      <i
        class="fa-sharp fa-solid fa-hand-holding-dollar rutTien"
        title="Rút Tiền"
        @click="ruttien"
        :class="{ on: this.BatDau }"
      ></i>
    </div>
  </div>
</template>

<script>
export default {
  name: "Funcition",
  data() {
    return {
      isDisabled: false,
    };
  },
  props: {
    BatDau: { type: Boolean, default: false },
  },
  methods: {
    admin() {
      this.$emit("xlAdmin");
    },
    ruttien() {
      this.$emit("xlRutTien");
    },
    naptien() {
      this.$emit("xlNap");
    },
    batdau() {
      this.$emit("xlBatDau");
      this.isDisabled = true;
    },
    luatchoi() {
      this.$emit("xlLuatChoi");
    },
    choilai() {
      this.$emit("xlChoiLai");
      console.log("a");
    },
  },
};
</script>

<style>
.Funcition {
  left: 2%;
  top: 25%;
  position: absolute;
  width: 660px;
  height: 1px;
  /* background-color: #000000; */
}
.batDauChoi.Stop {
  visibility: hidden;
}
.batDauChoi {
  width: 580px;
  height: 210px;
  border-radius: 110px;

  position: absolute;
  top: 100%;
  left: 50%;
  transform: translate(-50%, -5%);
  background-color: #3fbbec;
  /* border: 1px solid #000; */
  text-align: center;
  font-size: 50px;
  font-weight: bold;
  padding-top: 50px;

  /* visibility: hidden; */
}
.t {
  width: 40px;
  height: 200px;
  /* border: 1px solid #d807b8; */
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  position: absolute;
  top: 0;
}

.thanh1 {
  left: 0;
}
.thanh2 {
  right: 0;
}

.Funcition .t i {
  width: 45px;
  height: 45px;
  background: linear-gradient(to bottom, #2525ffe6, #58a6eb);
  border-radius: 50%;
  color: whitesmoke;
  border: 1px solid whitesmoke;
  cursor: pointer;

  display: flex;
  justify-content: center;
  align-items: center;

  transition: all 0.3s ease;
}
.Funcition .t i:hover {
  background: rgb(37, 37, 186);
}
.t .luatChoi {
  margin-left: -15px;
}
.t .napTien {
  margin-left: 18px;
}

.disabledBatDau {
  pointer-events: none;
  opacity: 0.5;
  /* cursor: not-allowed; */
}

.napTien,
.rutTien,
.choiLai {
  opacity: 0.5;
  pointer-events: none;
}

.napTien.on,
.rutTien.on,
.choiLai.on {
  pointer-events: auto;
  opacity: 1;
}
</style>
