<template>
  <div class="RutTien" :class="{ on: this.openRutTien }">
    <div class="rt">
      <h2>Tổng Tiền: {{ TongTienString }}</h2>
      <div class="infoNganHang">
        <label>Ngân Hàng:</label>

        <!-- sk @change được kích hoạt khi dc thay đổi, thông qua việc rời khỏi phần tử đó( thường là các tùy chọn trong select ) -->
        <select @change="chonnganhang">
          <option
            v-for="(i, index) in TenNganHang"
            :key="index"
            :selected="index === 0"
            :disabled="index === 0"
          >
            {{ i }}
          </option>
        </select>
        <label>Số Tài Khoản: </label>
        <input
          type="text"
          oninput="this.value = this.value.replace(/[^0-9]/g, '');"
          v-model="Input2"
        />
        <label>Người Hưởng Thụ: </label>
        <input
          type="text"
          oninput="this.value = this.value.replace(/[^a-zA-Z\s]/g, '');"
          v-model="Input3"
        />
      </div>
      <div class="nhapTien">
        <label for="">Số Tiền: </label>
        <input type="text" v-model="NhapTien" @input="chuyendoi()" />
      </div>
      <div class="buttonLuaChon">
        <button
          title="Số Tiền Phải Lớn Hơn 20.000.000"
          :style="{
            opacity: this.TongTien < 20000000 ? 0.5 : 1,
            cursor: this.TongTien < 20000000 ? 'not-allowed' : 'pointer',
          }"
          :disabled="this.TongTien < 20000000"
          @click="ruttien"
        >
          Rút Tiền
        </button>
        <button @click="$emit('xlRutTien')">Thoát</button>
      </div>
    </div>
    <div class="thongBao" :class="{ on: HienThiThongBao }">
      <strong>Hệ Thống Đang Bảo Trì, Vui Lòng Quay Lại Sau. </strong> <br />
      <button @click="ruttien">Ấu Kề</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "RutTien",
  data() {
    return {
      HienThiThongBao: false,
      Input1: null,
      Input2: null,
      Input3: null,
      HienThiRutTien: true,
      NhapTien: "",
      TenNganHang: [
        "Chọn Ngân Hàng",
        "MbBank",
        "VietcomBank",
        "BIDV",
        "Techcombank",
        "VietinBank",
        "ACB",
        "Sacombank",
        "VIB",
        "VPBank",
        "TPBank",
        "Agribank",
        "HDBank",
      ],
    };
  },
  props: {
    openRutTien: { tyoe: Boolean, default: false },
    TongTien: { type: Number, default: 0 },
  },
  computed: {
    TongTienString() {
      let tien = this.TongTien.toLocaleString("vi-VN", {});
      return tien;
    },
    KiemTra() {
      return (
        this.Input1 === null ||
        this.Input2 === null ||
        this.Input3 === null ||
        this.NhapTien === ""
      );
    },
  },
  methods: {
    ruttien() {
      if (this.KiemTra) {
        alert("Vui lòng điền đủ các thông tin.");
      } else {
        this.HienThiThongBao = !this.HienThiThongBao;
      }
    },

    chuyendoi() {
      let value = this.NhapTien.replace(/[^0-9]/g, "");
      this.NhapTien = Number(value).toLocaleString("de-DE");
    },
    chonnganhang() {
      this.Input1 = 123;
    },
  },
};
</script>

<style>
.RutTien {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(245, 245, 245, 0.479);
  transition: all 0.5s ease-out;

  opacity: 0;
  visibility: hidden;
}
.RutTien.on {
  opacity: 1;
  visibility: visible;
}

.rt {
  position: absolute;
  width: 300px;
  /* height: 200px; */
  border: 3px double rgba(40, 40, 255, 0.842);
  left: 40%;
  border-radius: 10px;
  transform: translate(-40%, 0);
  transition: all 0.5s ease-out;
  background: #f1f1f1;
}
.on .rt {
  transform: translate(-40%, 30%);
}

.RutTien h2 {
  color: rgb(38, 38, 255);
}
.infoNganHang {
  text-align: center;
}

.infoNganHang label,
.infoNganHang select,
.infoNganHang input {
  width: 45%;
  display: inline-block;
  margin-top: 15px;
}

.infoNganHang label {
  width: 90px;
  display: inline-block;
  width: 130px;
  text-align: left;
}
.infoNganHang input,
.infoNganHang select {
  margin-left: 5px;
}

.nhapTien {
  padding: 15px;
  display: flex;
  justify-content: space-between;
}
.nhapTien input {
  width: 210px;
}

.buttonLuaChon {
  display: flex;
  justify-content: space-around;
}
.buttonLuaChon button,
.thongBao button {
  padding: 7px 20px;
  margin: 5px 23px;
  border-radius: 10px;
  border: none;
  color: whitesmoke;
  background: var(--mauLinear);
  font-weight: 700;
  cursor: pointer;
  margin-bottom: 10px;
}
.buttonLuaChon button:hover,
.thongBao button:hover {
  background: var(--mauHover);
}

.RutTien input {
  border-top-left-radius: 10px;
  border-bottom-right-radius: 10px;
  height: 21px;
  font-weight: bold;
}

.thongBao {
  position: absolute;
  padding: 10px;
  border: 3px dashed red;
  width: 400px;
  /* height: 300px; */
  background-color: rgb(255, 255, 255);
  text-align: center;
  transform: translate(-40%, -35%);
  left: 40%;
  top: 35%;

  opacity: 0;
  visibility: hidden;
}
.thongBao.on {
  opacity: 1;
  visibility: visible;
}
.thongBao strong {
  font-size: 25px;
}
</style>
