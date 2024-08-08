<template>
  <div id="app">
    <display
      :HienThiTienDaCuoc="HienThiTienDaCuoc"
      :DisabledCuoc="DisabledCuoc"
      :TienCuoc="TienCuoc"
      :indexTenCuoc="indexTenCuoc"
      :ScaleTongTien="ScaleTongTien"
      :xlRandomTongTienCuoc="xlRandomTongTienCuoc"
      :SoNguoiChoi="SoNguoiChoi"
      :xlRandomTongTien="xlRandomTongTien"
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
    <luat-choi :openLuatChoi="openLuatChoi" @xlBatDau="xlBatDau" />
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
      RandomTongTien: "600000",
      HienThiTongTien: false,
      HienThiThoiGianVanMoi: false,
      ThoiGianVanMoi: 2,
      ThoiGianQuayXucXac: 5,
      TatHienThiThoiGian: false,
      ThoiGian: 10,
      openLuatChoi: false,
      BatDau: false,
      Dices: [3, 4, 6],
      datcuoc: ["1K", "10K", "50K", "100K", "500K", "1M", "10M", "50M"],
      itemsLi: Array(20).fill(""),
      liIndex: [3, 4, 6, 7, 11, 13, 14, 15, 19],
    };
  },
  components: {
    Display,
    Buttom,
    Funcition,
    LuatChoi,
  },
  computed: {
    xlRandomTongTien() {
      let tien = Math.floor(Math.random() * 1500000) + 150000;
      this.RandomTongTien = tien.toLocaleString("vi-VN", { style: "decimal" });
      // console.log(typeof this.RandomTongTien);
      this.TongTien = Number(this.RandomTongTien.replace(/\./g, ""));
      // console.log(typeof this.TongTien);
      // console.log(this.TongTien);

      return [this.RandomTongTien, this.TongTien];
    },

    xlRandomTongTienCuoc() {
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
    xlHuy(e) {
      console.log("e = " + e);

      if (e === "huy") {
        this.DisabledCuoc = false;
        this.TienCuoc = 0;
      } else if (e === "datcuoc") {
        this.DisabledCuoc = true;
        this.HienThiTienDaCuoc[0] = this.HienThiTienDaCuoc[0] === 1 ? 2 : 0;
        this.HienThiTienDaCuoc[1] = this.HienThiTienDaCuoc[1] === 1 ? 3 : 0; // dựa vào tham số xlCuocTien(e)
      }
      this.indexTenCuoc[0] = this.indexTenCuoc[1] = 0;
      this.HienThiFileButton = false;
    },
    xlMenuCuoc(e) {
      let tiencuoc;
      if (e.includes("K")) {
        tiencuoc = e.replace(/(\d+)K/, (match, p1) => {
          return p1 * 1000;
        });
      } else {
        tiencuoc = e.replace(/(\d+)M/, (match, p1) => {
          return p1 * 1000000;
        });
      }
      tiencuoc = Number(tiencuoc);
      console.log("tiencuoc = " + tiencuoc);

      this.TienCuoc += tiencuoc;
    },

    xlCuocTien(e) {
      this.DisabledCuoc = this.HienThiFileButton = true;
      this.indexTenCuoc[e] = this.HienThiTienDaCuoc[e] = 1;
    },
    xlThoiGian() {
      let ThoiGian2 = this.ThoiGian;
      // this.xlSoNguoiChoi_xlTongTienCuoc(ThoiGian2, this.SoNguoiChoi[0], 5, 20);
      this.xlSoNguoiChoi_xlTongTienCuoc(
        ThoiGian2,
        this.SoNguoiChoi[0],
        this.TongTienCuoc[0],
        100000,
        50000000,
        900,
        this.ScaleTongTien[0]
      );
      this.xlSoNguoiChoi_xlTongTienCuoc(
        ThoiGian2,
        this.SoNguoiChoi[1],
        this.TongTienCuoc[1],
        100000,
        50000000,
        850,
        this.ScaleTongTien[1]
      );
      let tg = setInterval(() => {
        if (this.ThoiGian-- === 0) {
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
            Math.floor((Math.random() * max) / 2000000) + min / 20000;
          tongTienCuoc.value += Math.floor(Math.random() * max) + min;

          if (x2TimeSoNguoiChoi) {
            timeSoNguoiChoi *= 2;
            x2TimeSoNguoiChoi = false;
            lapLan1 = 1;
          }

          timeSoNguoiChoi--;
          if (timeSoNguoiChoi === 5 && lapLan1 === 0) {
            startInterval(500);
            x2TimeSoNguoiChoi = true;
          } else if (timeSoNguoiChoi <= 0) {
            clearInterval(count);
          }
        }, newTime);
      }

      startInterval(time);
    },

    quayXucXac(time) {
      let { ThoiGianQuayXucXac } = this;
      ThoiGianQuayXucXac = time;

      let qxx = setInterval(() => {
        let d1 = Math.floor(Math.random() * 6) + 1;
        let d2 = Math.floor(Math.random() * 6) + 1;
        let d3 = Math.floor(Math.random() * 6) + 1;

        this.Dices = [d1, d2, d3];
        ThoiGianQuayXucXac--;
        if (ThoiGianQuayXucXac === 1) {
          clearInterval(qxx);

          ThoiGianQuayXucXac = time;
          let count = 2;
          let doTre = setInterval(() => {
            if (count-- === 1) {
              clearInterval(doTre);
              this.xlThoiGianVanMoi(this.ThoiGianVanMoi);
            }
          }, 1000);
        }
      }, 500);
    },

    quayXucXac(time) {
      let { ThoiGianQuayXucXac } = this;
      ThoiGianQuayXucXac = time;

      let qxx = setInterval(() => {
        let d1 = Math.floor(Math.random() * 6) + 1;
        let d2 = Math.floor(Math.random() * 6) + 1;
        let d3 = Math.floor(Math.random() * 6) + 1;

        this.Dices = [d1, d2, d3];
        ThoiGianQuayXucXac--;
        if (ThoiGianQuayXucXac === 1) {
          clearInterval(qxx);

          ThoiGianQuayXucXac = time;
          let count = 2;
          let doTre = setInterval(() => {
            if (count-- === 1) {
              clearInterval(doTre);
              this.xlThoiGianVanMoi(this.ThoiGianVanMoi);
            }
          }, 1000);
        }
      }, 500);
    },
    xlThoiGianVanMoi(time) {
      this.HienThiThoiGianVanMoi = !this.HienThiThoiGianVanMoi; // display time Dices

      let tgvm = setInterval(() => {
        this.ThoiGianVanMoi--;
        if (this.ThoiGianVanMoi === 0) {
          this.HienThiTienDaCuoc[0] =
            this.HienThiTienDaCuoc[1] =
            this.TienCuoc =
              0;
          this.DisabledCuoc = false;
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
      this.openLuatChoi = true;
    },
    xlBatDau() {
      this.BatDau = true;
      this.openLuatChoi = false;
      this.HienThiTongTien = true;
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
