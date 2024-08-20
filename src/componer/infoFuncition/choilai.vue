<template>
  <div class="ChoiLai" :class="{ on: this.openChoiLai }">
    <div class="cl">
      <h3>
        Nhận lượt chơi lại tiếp theo trong khoảng:
        {{ HienThi }} nữa.
      </h3>
      <h3>Lượt chơi lại còn: {{ this.LuotChoi1 }} lượt.</h3>
      <button
        class="choilai"
        @click="choilai"
        :style="{
          opacity: this.LuotChoi1 > 0 ? 1 : 0.5,
          cursor: this.LuotChoi1 > 0 ? 'pointer' : 'not-allowed',
        }"
        :disabled="this.LuotChoi1 < 1"
      >
        Chơi Lại
      </button>
      <button class="thoat" @click="thoat">Thoát</button>
    </div>
    <div class="xacnhanchoilai" :class="{ on: XacNhanChoiLai }">
      <h2>Bạn có chắc chắn chơi lại?</h2>
      <button @click="yesChoiLai">Yes</button>
      <button @click="choilai">No</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "ChoiLai",
  data() {
    return {
      XacNhanChoiLai: false,
      TimeLuotChoiLai: this.tinhSoPhutRaGiay(15), // 0.1 = 6s, 1 = 1p, 10 = 10p
    };
  },
  props: {
    LuotChoi1: { type: Number, default: 0 },
    openChoiLai: { type: Boolean, default: false },
  },
  computed: {
    HienThi() {
      const phut = Math.floor(this.TimeLuotChoiLai / 60);
      const giay = this.TimeLuotChoiLai % 60;
      return `${this.hienThiTime(phut)}:${this.hienThiTime(giay)}`;
    },
  },
  mounted() {
    this.startDem();
  },
  methods: {
    hienThiTime(time) {
      return time < 10 ? `0${time}` : time;
    },
    tinhSoPhutRaGiay(min) {
      return min * 60;
    },
    startDem() {
      let start = setInterval(() => {
        if (this.TimeLuotChoiLai-- <= 1) {
          clearInterval(start);
          this.$emit("xlTangLuot", "choilai");
          this.TimeLuotChoiLai = this.tinhSoPhutRaGiay(15);
          this.startDem();
        }
      }, 1000);
    },
    thoat() {
      this.$emit("xlChoiLai", "choilai");
    },
    choilai() {
      this.XacNhanChoiLai = !this.XacNhanChoiLai;
    },
    yesChoiLai() {
      this.$emit("xlReset");
      this.choilai(); // tắt yesChoiLai
    },
  },
};
</script>

<style>
:root {
  --mauHover: rgb(37, 37, 186);
  --mauLinear: linear-gradient(to bottom, #0000ff, #87ceeb);
}
.ChoiLai {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(93, 147, 227, 0.461);
  opacity: 0;
  visibility: hidden;
  transition: all 0.5s ease;
}
.ChoiLai.on {
  visibility: visible;
  opacity: 1;
}
.cl {
  position: absolute;
  top: 30%;
  left: 50%;
  transform: translate(-50%, -30%) scale(1.3);
  border: 3px double #0000ff;
  padding: 10px;
  width: 300px;
  line-height: 1.5;
  border-radius: 17px;
  background: rgb(241, 244, 246);
  transition: all 0.5s ease;
}

.on .cl {
  transform: translate(-50%, -30%) scale(1);
}
.ChoiLai button {
  padding: 7px 20px;
  margin: 10px 23px;
  border-radius: 10px;
  border: none;
  color: whitesmoke;
  background: var(--mauLinear);
  font-weight: 700;
  cursor: pointer;
}
.ChoiLai button:hover {
  background: var(--mauHover);
}
.xacnhanchoilai {
  display: inline-block;
  border: 1px solid #000;
  position: absolute;
  top: 40%;
  left: 0%;
  /* transform: translate(-50%, -40%); */
  transform: translateY(-40%);
  background-color: #fff;
  padding: 10px;
  border-radius: 10px;
  border: 3px double #1d1d20;

  opacity: 0;
  visibility: hidden;
  transition: all 0.2s ease;
}
.xacnhanchoilai.on {
  opacity: 1;
  visibility: visible;

  position: absolute;
  top: 40%;
  left: 50%;
  transform: translate(-50%, -40%);
}
</style>
