<template>
  <div id="app">
    <display
      :HienThiTienThuong="HienThiTienThuong"
      :KQ="KQ"
      :TongTienString="TongTienString"
      :HienThiTienDaCuoc="HienThiTienDaCuoc"
      :DisabledCuoc="DisabledCuoc"
      :TienCuoc="TienCuoc"
      :indexTenCuoc="indexTenCuoc"
      :ScaleTongTien="ScaleTongTien"
      :xlTongTienStringCuoc="xlTongTienStringCuoc"
      :SoNguoiChoi="SoNguoiChoi"
      :HienThiTongTien="HienThiTongTien"
      @xlCuocTien="xlCuocTien"
      :HienThiThoiGianVanMoi="HienThiThoiGianVanMoi"
      :ThoiGianVanMoi="ThoiGianVanMoi"
      :TatHienThiThoiGian="TatHienThiThoiGian"
      :ThoiGian="ThoiGian"
      :itemsLi="itemsLi"
      :liIndex="liIndex"
      :BatDau="BatDau"
      :Dices="Dices"
    />

    <buttom
      :DisabledAll="DisabledAll"
      :TongTien="TongTien"
      :HienThiFileButton="HienThiFileButton"
      @xlHuy="xlHuy"
      @xlMenuCuoc="xlMenuCuoc"
      :datcuoc="datcuoc"
    />

    <funcition
      @xlThoiGian="xlThoiGian"
      @xlBatDau="xlBatDau"
      :BatDau="BatDau"
      @xlLuatChoi="xlLuatChoi"
    />
    <luat-choi :openLuatChoi="openLuatChoi" @xlLuatChoi="xlLuatChoi" />
  </div>
</template>

<script>
import LuatChoi from "./componer/infoFuncition/luatchoi.vue";
import Display from "./componer/display.vue";
import Buttom from "./componer/buttom.vue";
import Funcition from "./componer/funcition.vue";
export default {
  tongTienCuoc: "App",
  data() {
    return {
      DisabledAll: false,
      HienThiTienThuong: null,
      KQ: "",
      HienThiTienDaCuoc: [0, 0],
      DisabledCuoc: false,
      TienCuoc: 0,
      indexTenCuoc: [0, 0],
      HienThiFileButton: false,

      ScaleTongTien: [{ scale: false }, { scale: false }],
      HienThiTongTienCuoc: ["0", "0"],
      TongTienCuoc: [{ value: 0 }, { value: 0 }],
      SoNguoiChoi: [{ value: 0 }, { value: 0 }],
      TongTien: 300000,
      TongTienString: "600000",
      HienThiTongTien: false,
      HienThiThoiGianVanMoi: false,
      TatHienThiThoiGian: false,
      openLuatChoi: false,
      BatDau: false,
      Dices: [3, 4, 6],
      datcuoc: ["1K", "10K", "50K", "100K", "500K", "1M", "10M", "50M"],
      itemsLi: Array(20).fill(""),
      liIndex: [3, 4, 6, 7, 11, 13, 14, 15, 19],

      ThoiGianVanMoi: 5,
      ThoiGianQuayXucXac: 5,
      ThoiGian: 10,
      BuffTienMin: 1000,
      BuffTienMax: 5000000,
    };
  },
  components: {
    Display,
    Buttom,
    Funcition,
    LuatChoi,
  },
  computed: {
    xlTongTienStringCuoc() {
      this.HienThiTongTienCuoc[0] = this.TongTienCuoc[0].value.toLocaleString(
        "vi-VN",
        {
          style: "decimal",
        }
      );
      this.HienThiTongTienCuoc[1] = this.TongTienCuoc[1].value.toLocaleString(
        "vi-VN",
        {
          style: "decimal",
        }
      );
      return this.HienThiTongTienCuoc;
    },
  },
  methods: {
    xlTongTienString() {
      let tien = Math.floor(Math.random() * (1500000 - 150000 + 1)) + 150000;
      this.TongTien = Number(tien);
      this.TongTienString = this.TongTien.toLocaleString("vi-VN", {
        style: "decimal",
      });
    },
    xlHuy(e) {
      console.log("e = " + e);

      if (e === "huy") {
        this.TongTien += this.TienCuoc;
        this.TienCuoc = 0;
        this.DisabledCuoc = this.DisabledAll = false;
      } else if (e === "datcuoc") {
        this.TongTienString = this.TongTien.toLocaleString("vi-VN", {
          style: "decimal",
        });

        this.DisabledCuoc = true;
        this.HienThiTienDaCuoc[0] = this.HienThiTienDaCuoc[0] === 1 ? 2 : 0;
        this.HienThiTienDaCuoc[1] = this.HienThiTienDaCuoc[1] === 1 ? 3 : 0; // dựa vào tham số xlCuocTien(e)
        if ("0" === this.TongTienString) {
          this.TongTien = 0;
        }
      } else if (e === "all") {
        this.TienCuoc = this.TongTien;
        this.TongTien = 0;
        this.DisabledAll = true;
        return;
      }
      this.indexTenCuoc[0] = this.indexTenCuoc[1] = 0;
      this.HienThiFileButton = false;
    },
    xlMenuCuoc(e) {
      let tiencuoc = parseFloat(e);
      if (e.includes("K")) {
        tiencuoc *= 1000;
      } else {
        tiencuoc *= 1000000;
      }
      tiencuoc = Number(tiencuoc);
      console.log("tiencuoc = " + tiencuoc);

      this.TienCuoc += tiencuoc;
      this.TongTien -= tiencuoc;

      this.DisabledAll = true;
    },

    xlCuocTien(e) {
      this.DisabledCuoc = this.HienThiFileButton = true;
      this.indexTenCuoc[e] = this.HienThiTienDaCuoc[e] = 1;

      if (e === 0) {
        this.HienThiTienDaCuoc[1] = 0;
      } else {
        this.HienThiTienDaCuoc[0] = 0;
      } // kết hợp với xlHuy(e) -> else ì(e=== 'datcuoc'), sk này xảy ra khi ng dùng chọn cược1 xong hủy, rồi chọn cuọc2
    },
    xlThoiGian() {
      let ThoiGian2 = this.ThoiGian;

      let time1 = Math.ceil(ThoiGian2 - ThoiGian2 * 0.9); // bổ sung thêm thời gian, setTimeOut là 900, suy ra 10s sẽ băgn 9s,
      let time2 = Math.ceil(ThoiGian2 - ThoiGian2 * 0.85);

      this.xlSoNguoiChoi_xlTongTienCuoc(
        ThoiGian2 + time1,
        this.SoNguoiChoi[0],
        this.TongTienCuoc[0],
        this.BuffTienMin,
        this.BuffTienMax,
        900,
        this.ScaleTongTien[0]
      );
      this.xlSoNguoiChoi_xlTongTienCuoc(
        ThoiGian2 + time2,
        this.SoNguoiChoi[1],
        this.TongTienCuoc[1],
        this.BuffTienMin,
        this.BuffTienMax,
        850,
        this.ScaleTongTien[1]
      );
      let tg = setInterval(() => {
        if (this.ThoiGian-- === 1) {
          clearInterval(tg);
          this.TatHienThiThoiGian = !this.TatHienThiThoiGian;
          this.quayXucXac(this.ThoiGianQuayXucXac * 2);
          this.ThoiGian = ThoiGian2;
        }
      }, 1000);
    },

    xlSoNguoiChoi_xlTongTienCuoc(
      timeSoNguoiChoi,
      soNguoiChoi,
      tongTienCuoc,
      min,
      max,
      time,
      ScaleTongTien
    ) {
      let count,
        x2TimeSoNguoiChoi = false,
        lapLan1 = 0;

      function startInterval(newTime) {
        if (count) {
          clearInterval(count);
        }

        count = setInterval(() => {
          ScaleTongTien.scale = !ScaleTongTien.scale;

          soNguoiChoi.value +=
            Math.floor(Math.random() * ((max - min + 1) / 1000000)) +
            min / 1000; // từ 1 - 20
          tongTienCuoc.value +=
            Math.floor(Math.random() * (max - min + 1)) + min; // từ 1.000 - 20.000.000

          if (x2TimeSoNguoiChoi) {
            timeSoNguoiChoi *= 2;
            x2TimeSoNguoiChoi = false; //chỉ vào đc 1 lần hàm này
            lapLan1 = 1; //ngn đk if tiếp theo chỉ vàp lần đầu
          }

          timeSoNguoiChoi--;
          if (timeSoNguoiChoi === 10 && lapLan1 === 0) {
            startInterval(500);
            x2TimeSoNguoiChoi = true;
          } else if (timeSoNguoiChoi <= 3) {
            clearInterval(count);
          }
        }, newTime);
      }

      startInterval(time);
    },

    quayXucXac(time) {
      let { ThoiGianQuayXucXac } = this;
      ThoiGianQuayXucXac = time;
      this.xlHetThoiGian();

      let qxx = setInterval(() => {
        let d1 = Math.floor(Math.random() * 6) + 1;
        let d2 = Math.floor(Math.random() * 6) + 1;
        let d3 = Math.floor(Math.random() * 6) + 1;
        let sumDices = d1 + d2 + d3;

        this.Dices = [d1, d2, d3];
        ThoiGianQuayXucXac--;
        if (ThoiGianQuayXucXac === 1) {
          clearInterval(qxx);
          if (sumDices >= 4 && sumDices <= 10) {
            this.KQ = "xiu";
            if (this.HienThiTienDaCuoc[1] === 3) {
              var tienThuong = Math.ceil(1.95 * this.TienCuoc);
              this.TongTien += tienThuong;
              this.TongTienString = this.TongTien.toLocaleString("vi-VN", {
                style: "decimal",
              });
              this.HienThiTienThuong = tienThuong.toLocaleString("vi-VN", {
                style: "decimal",
              });
            }
          } else if (sumDices >= 11 && sumDices <= 17) {
            this.KQ = "tai";
            if (this.HienThiTienDaCuoc[0] === 2) {
              var tienThuong = Math.ceil(1.95 * this.TienCuoc);
              this.TongTien += tienThuong;
              this.TongTienString = this.TongTien.toLocaleString("vi-VN", {
                style: "decimal",
              });
              this.HienThiTienThuong = tienThuong.toLocaleString("vi-VN", {
                style: "decimal",
              });
            }
          }

          ThoiGianQuayXucXac = time;
          let count = 2; // khựng trong 2s đẻ hiển thị thời gian ván mới
          let doTre = setInterval(() => {
            if (count-- === 1) {
              clearInterval(doTre);
              this.xlThoiGianVanMoi(this.ThoiGianVanMoi);
            }
          }, 1000);
        }
      }, 500);
    },

    xlHetThoiGian() {
      this.DisabledCuoc = true;
      this.HienThiFileButton = false;
      this.indexTenCuoc[0] = this.indexTenCuoc[1] = 0;
    },
    xlThoiGianVanMoi(time) {
      this.HienThiThoiGianVanMoi = !this.HienThiThoiGianVanMoi; // display time Dices

      let tgvm = setInterval(() => {
        this.ThoiGianVanMoi--;
        if (this.ThoiGianVanMoi === 0) {
          this.HienThiTienThuong = null;
          this.KQ = "";
          this.HienThiTienDaCuoc[0] =
            this.HienThiTienDaCuoc[1] =
            this.TienCuoc =
              0;
          this.DisabledCuoc = this.DisabledAll = false;
          clearInterval(tgvm);
          this.SoNguoiChoi[0].value = this.SoNguoiChoi[1].value = 0;
          this.TongTienCuoc[0].value = this.TongTienCuoc[1].value = 0;
          this.xlThoiGian();
          this.ThoiGianVanMoi = time;
          this.HienThiThoiGianVanMoi = !this.HienThiThoiGianVanMoi; // close time Dices
          this.TatHienThiThoiGian = !this.TatHienThiThoiGian;
        }
      }, 1000);
    },

    xlLuatChoi() {
      this.openLuatChoi = !this.openLuatChoi;
    },
    xlBatDau() {
      this.BatDau = true;
      this.HienThiTongTien = true;
      this.xlTongTienString();
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
