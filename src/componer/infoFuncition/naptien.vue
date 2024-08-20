<template>
  <div class="NapTien" :class="{ on: this.openNap }">
    <div class="nt">
      <h3>Nhận lượt nạp tiền tiếp theo trong khoảng: {{ HienThi }} nữa.</h3>
      <h3>Nạp tiền còn lại: {{ this.LuotNap }} lượt.</h3>

      <label>Số Tiền: </label>
      <input
        class="range"
        type="range"
        v-model="Tien"
        min="1000"
        max="500000"
      />
      <strong>{{ soTien }}</strong> <br />

      <button
        class="nap"
        @click="nap"
        :style="{
          opacity: this.LuotNap > 0 ? 1 : 0.5,
          cursor: this.LuotNap > 0 ? 'pointer' : 'not-allowed',
        }"
        :disabled="this.LuotNap < 1"
      >
        Nạp
      </button>
      <button class="thoat" @click="thoat">Thoát</button>
    </div>
    <div class="xacnhannap" :class="{ on: XacNhanNap }">
      <h2>Bạn có chắc chắn nạp {{ soTien }} ?</h2>
      <button @click="yesNap">Yes</button>
      <button @click="nap">No</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "NapTien",
  data() {
    return {
      Tien: 1000,
      XacNhanNap: false,
      TimeLuotNap: this.tinhSoPhutRaGiay(14.5), // 0.1 = 6s, 1 = 1p, 10 = 10p
    };
  },
  props: {
    LuotNap: { type: Number, default: 1 },
    openNap: { type: Boolean, default: false },
  },
  computed: {
    soTien() {
      let numberTien = Number(this.Tien);
      return numberTien.toLocaleString("vi-VN");
    },
    HienThi() {
      const phut = Math.floor(this.TimeLuotNap / 60);
      const giay = this.TimeLuotNap % 60;
      return `${this.hienThiTime(phut)}:${this.hienThiTime(giay)}`;
    },
  },
  mounted() {
    //tự động chạy khi được gọi file này
    this.startDem();
  },
  methods: {
    yesNap() {
      let numberTien = Number(this.Tien);
      this.$emit("xlNapTien", numberTien);
      this.nap();
    },
    nap() {
      this.XacNhanNap = !this.XacNhanNap;
    },

    thoat() {
      this.$emit("xlNap");
    },

    hienThiTime(time) {
      return time < 10 ? `0${time}` : time;
    },
    tinhSoPhutRaGiay(min) {
      return min * 60;
    },

    startDem() {
      let start = setInterval(() => {
        if (this.TimeLuotNap-- <= 1) {
          clearInterval(start);
          this.$emit("xlTangLuot", "naptien");
          this.TimeLuotNap = this.tinhSoPhutRaGiay(15);
          this.startDem();
        }
      }, 1000);
    },
  },
};
</script>

<style>
.NapTien {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #6da9cb6f;
  transition: all 0.5s ease-in;

  opacity: 0;
  visibility: hidden;
}
.nt {
  position: absolute;
  top: 30%;
  border: 3px double rgba(40, 40, 255, 0.842);
  width: 500px;
  transform: translateY(-40%);
  padding: 10px;
  line-height: 1.5;
  background: rgb(241, 244, 246);
  border-radius: 5px;
  transition: all 0.3s ease;
}
.NapTien.on {
  opacity: 1;
  visibility: visible;
}
.on .nt {
  transform: translate(40%, -40%);
}

.NapTien button {
  padding: 7px 20px;
  margin: 5px 23px;
  border-radius: 10px;
  border: none;
  color: whitesmoke;
  background: var(--mauLinear);
  font-weight: 700;
  cursor: pointer;
}
.NapTien button:hover {
  background: var(--mauHover);
}

.xacnhannap {
  position: absolute;
  border: 1px solid rgba(40, 40, 255, 0.661);
  display: inline-block;
  top: 32%;
  line-height: 1.2;
  transform: translate(0, -32%);
  transition: all 0.3s ease;
  background-color: white;
  border-radius: 10px;

  opacity: 0;
  visibility: hidden;
}
.xacnhannap.on {
  left: 10%;
  transform: translateX(45%);
  opacity: 1;
  visibility: visible;
}
</style>
