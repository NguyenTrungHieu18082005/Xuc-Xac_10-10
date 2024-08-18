<template>
  <div class="Button" :class="{ on: this.HienThiFileButton }">
    <div class="menuTienCuoc">
      <ul>
        <li
          class="liDatCuoc"
          v-for="(i, id) in filteredDatCuoc"
          :key="id"
          @click="click(i.TenMenuButton)"
        >
          <button
            :style="{
              opacity: i.isDisabled ? 0.5 : 1,
              cursor: i.isDisabled ? 'not-allowed' : 'pointer',
            }"
            :disabled="i.isDisabled"
          >
            {{ i.TenMenuButton }}
          </button>
        </li>
      </ul>
    </div>

    <div class="chucnangButton">
      <button
        class="button-blue"
        @click="huy('all')"
        :style="{
          opacity: this.DisabledAll || this.TongTien < 1 ? 0.5 : 1, // DisabledAll: ẩn all khi nhấn button menu. TongTien: ẩn all khi tiền về 0 (áp dung ván mới)
          cursor:
            this.DisabledAll || this.TongTien < 1 ? 'not-allowed' : 'pointer',
        }"
        :disabled="this.DisabledAll || this.TongTien < 1"
      >
        TẤT CẢ
      </button>
      <button
        class="button-gold"
        :style="{
          opacity: this.TongTienString < 1 ? 0.5 : 1,
          cursor: this.TongTienString < 1 ? 'not-allowed' : 'pointer',
        }"
        :disabled="this.TongTienString < 1"
        @click="huy('datcuoc')"
      >
        ĐẶT CƯỢC
      </button>
      <button class="button-red" @click="huy('huy')">HỦY</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Button",
  props: {
    TongTienString: { type: String, default: "0" },
    DisabledAll: { type: Boolean, default: false },
    TongTien: { type: Number, default: 0 },
    HienThiFileButton: { type: Boolean, default: false },
    datcuoc: { type: Array, default: null },
  },
  computed: {
    filteredDatCuoc() {
      return this.datcuoc.map((i) => ({
        TenMenuButton: i,
        isDisabled: this.convertToNumber(i) > this.TongTien,
      }));
    },
    a() {
      return this.TongTien <= 0;
    },
  },
  methods: {
    convertToNumber(str) {
      let value = parseFloat(str);
      if (str.includes("K")) {
        value *= 1000;
      } else if (str.includes("M")) {
        value *= 1000000;
      }
      return value;
    },
    huy(e) {
      this.$emit("xlHuy", e);
    },
    click(i) {
      this.$emit("xlMenuCuoc", i);
    },
  },
};
</script>

<style>
.Button {
  top: 90%;
  left: 7%;
  transform: translateY(-90%);
  /* background-color: #489a1868; */
  width: 600px;
  height: 30px;
  position: absolute;
  opacity: 0;
  visibility: hidden;
}
.Button.on {
  opacity: 1;
  visibility: visible;
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
