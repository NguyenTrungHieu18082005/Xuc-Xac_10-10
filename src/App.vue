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
      :TongTienString="TongTienString"
      :DisabledAll="DisabledAll"
      :TongTien="TongTien"
      :HienThiFileButton="HienThiFileButton"
      @xlHuy="xlHuy"
      @xlMenuCuoc="xlMenuCuoc"
      :datcuoc="datcuoc"
    />

    <funcition
      @xlAdmin="xlAdmin"
      @xlRutTien="xlRutTien"
      @xlNap="xlNap"
      @xlChoiLai="xlChoiLai"
      @xlBatDau="xlBatDau"
      :BatDau="BatDau"
      @xlLuatChoi="xlLuatChoi"
    />
    <luat-choi
      :BatDau="BatDau"
      :openLuatChoi="openLuatChoi"
      @xlLuatChoi="xlLuatChoi"
    />

    <choi-lai
      @xlTangLuot="xlTangLuot"
      :LuotChoi1="LuotChoi1"
      @xlReset="xlReset"
      :openChoiLai="openChoiLai"
      @xlChoiLai="xlChoiLai"
    />

    <nap-tien
      @xlTangLuot="xlTangLuot"
      :LuotNap="LuotNap"
      @xlNapTien="xlNapTien"
      @xlNap="xlNap"
      :openNap="openNap"
    />

    <rut-tien
      :openRutTien="openRutTien"
      @xlRutTien="xlRutTien"
      :TongTien="TongTien"
    />

    <admin
      @xlKieuHack="xlKieuHack"
      @xlAdminBuff="xlAdminBuff"
      @xlAdmin="xlAdmin"
      :openAdmin="openAdmin"
    />
  </div>
</template>

<script>
import Admin from "./componer/infoFuncition/admin.vue";
import RutTien from "./componer/infoFuncition/ruttien.vue";
import NapTien from "./componer/infoFuncition/naptien.vue";
import ChoiLai from "./componer/infoFuncition/choilai.vue";
import LuatChoi from "./componer/infoFuncition/luatchoi.vue";
import Display from "./componer/display.vue";
import Buttom from "./componer/buttom.vue";
import Funcition from "./componer/funcition.vue";

export default {
  name: "App",
  data() {
    return {
      KieuHack: "buff",

      arrayTai: [],
      arrayXiu: [],

      LuotNap: 1,
      LuotChoi1: 1,

      openAdmin: false,
      openRutTien: false,
      openNap: false,
      openChoiLai: false,

      DisabledAll: false,
      HienThiTienThuong: null,
      KQ: "", //hiển thị tài hay xỉu thắng
      HienThiTienDaCuoc: [0, 0],
      DisabledCuoc: false,
      DatCuoc: false,
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
      sumDices: null,
      Dices: [3, 4, 6],
      datcuoc: ["1K", "10K", "50K", "100K", "500K", "1M", "10M", "50M"],
      itemsLi: Array(20).fill(""),
      liIndex: [3, 4, 6, 7, 11, 13, 14, 15, 19],

      ThoiGianVanMoi: 5,
      ThoiGianQuayXucXac: 5,
      ThoiGian: 60,
      ThoiGianDuocSua: null,
      BuffTienMin: 1000,
      BuffTienMax: 30000000,

      ArraySetInterval: [],
    };
  },
  components: {
    Admin,
    RutTien,
    NapTien,
    ChoiLai,
    LuatChoi,
    Funcition,
    Buttom,
    Display,
  },
  computed: {
    xlTongTienStringCuoc() {
      this.HienThiTongTienCuoc[0] =
        this.TongTienCuoc[0].value.toLocaleString("vi-VN");
      this.HienThiTongTienCuoc[1] =
        this.TongTienCuoc[1].value.toLocaleString("vi-VN");
      return this.HienThiTongTienCuoc;
    },
  },
  methods: {
    xlKieuHack(e) {
      this.KieuHack = e;
    },
    xlBuffWin() {
      return Math.floor(Math.random() * 10) + 1;
    },
    KetQuaQuay() {
      if (this.sumDices <= 10) {
        this.KQ = "xiu";
        if (this.HienThiTienDaCuoc[1] === 3) {
          this.CongTienThang();
        }
      } else if (this.sumDices >= 11) {
        this.KQ = "tai";
        if (this.HienThiTienDaCuoc[0] === 2) {
          this.CongTienThang();
        }
      }
    },
    xl010() {
      this.ThangThua();
    },
    CongTienThang() {
      let tienThuong = Math.ceil(1.95 * this.TienCuoc);
      this.TongTien += tienThuong;
      this.TongTienString = this.TongTien.toLocaleString("vi-VN", {});
      this.HienThiTienThuong = tienThuong.toLocaleString("vi-VN", {});
    },
    xl100() {
      console.log(" ");

      if (this.HienThiTienDaCuoc[0] === 2) {
        console.log("Tai: " + this.arrayTai);

        this.Dices = [this.arrayTai[0], this.arrayTai[1], this.arrayTai[2]];
        console.log("dices tai2: " + this.Dices);

        this.KQ = "tai";
        console.log("tai thang");
        this.CongTienThang();
      } else {
        console.log("Xiu: " + this.arrayXiu);

        this.Dices = [this.arrayXiu[0], this.arrayXiu[1], this.arrayXiu[2]];
        console.log("dices xiu2: " + this.Dices);

        this.KQ = "xiu";
        console.log("xiu thang");
        this.CongTienThang();
      }
    },
    QuayBuffXucXac() {
      console.log("quay xuc xac");
      console.log("Dices: " + this.Dices);
      console.log("arrayTai: " + this.arrayTai);
      console.log("arrayXiu: " + this.arrayXiu);
      console.log("Length Tai: " + this.arrayTai.length);
      console.log("Length Xiu: " + this.arrayXiu.length);

      let d = 1;
      let qxx = setInterval(() => {
        let d1 = Math.floor(Math.random() * 6) + 1;
        let d2 = Math.floor(Math.random() * 6) + 1;
        let d3 = Math.floor(Math.random() * 6) + 1;
        let sum = d1 + d2 + d3;

        if (sum >= 11 && this.arrayTai.length < 3) {
          this.arrayTai.push(d1, d2, d3);
          console.log(`arrayTai(${d++}): ` + this.arrayTai + " = " + sum);
        } else if (sum <= 10 && this.arrayXiu.length < 3) {
          this.arrayXiu.push(d1, d2, d3);
          console.log(`arrayXiu(${d++}): ` + this.arrayXiu + " = " + sum);
        }

        if (this.arrayTai.length >= 3 && this.arrayXiu.length >= 3) {
          clearInterval(qxx);
          console.log(
            `Final Result: Tai - ${this.arrayTai.length}, Xiu - ${this.arrayXiu.length}`
          );
        }
      }, 100);
    },

    xl91(so) {
      console.log("so: " + so);
      if (so <= 9) {
        console.log("ket qua quay");
        this.KetQuaQuay();
      } else {
        console.log("thang thua");
        this.ThangThua();
      }
    },
    xl73(so) {
      console.log("so: " + so);
      if (so <= 7) {
        console.log("ket qua quay");
        this.KetQuaQuay();
      } else {
        console.log("thang thua");
        this.ThangThua();
      }
    },
    xl37(so) {
      if (so <= 3) {
        console.log("ket qua quay");
        this.KetQuaQuay();
      } else {
        console.log("thang thua");
        this.ThangThua();
      }
    },
    xl55(so) {
      console.log("so: " + so);
      if (so <= 5) {
        console.log("ket qua quay");
        this.KetQuaQuay();
      } else {
        console.log("thang thua");
        this.ThangThua();
      }
    },
    xl82(so) {
      console.log("so: " + so);
      if (so <= 8) {
        console.log("ket qua quay");
        this.KetQuaQuay();
      } else {
        console.log("thang thua");
        this.ThangThua();
      }
    },
    xl64(so) {
      console.log("so: " + so);
      if (so <= 6) {
        console.log("ket qua quay");
        this.KetQuaQuay();
      } else {
        console.log("thang thua");
        this.ThangThua();
      }
    },
    xl46(so) {
      console.log("so: " + so);
      if (so <= 4) {
        console.log("ket qua quay");
        this.KetQuaQuay();
      } else {
        console.log("thang thua");
        this.ThangThua();
      }
    },
    xl28(so) {
      console.log("so: " + so);
      if (so <= 2) {
        console.log("ket qua quay");
        this.KetQuaQuay();
      } else {
        console.log("thang thua");
        this.ThangThua();
      }
    },

    ThangThua() {
      console.log("vao thangthua");
      let qxx = setInterval(() => {
        let s1 = Math.floor(Math.random() * 6) + 1;
        let s2 = Math.floor(Math.random() * 6) + 1;
        let s3 = Math.floor(Math.random() * 6) + 1;

        let sum = s1 + s2 + s3;
        if (sum > 10 && this.arrayTai.length < 3) {
          this.arrayTai.push(s1, s2, s3);
        } else if (sum < 11 && this.arrayXiu.length < 3) {
          this.arrayXiu.push(s1, s2, s3);
        }

        if (this.arrayTai.length >= 3 && this.arrayXiu.length >= 3) {
          clearInterval(qxx);
        }
      }, 100);

      if (this.HienThiTienDaCuoc[1] === 3) {
        this.Dices = [this.arrayTai[0], this.arrayTai[1], this.arrayTai[2]];
        this.KQ = "tai";
        console.log("tai thang");
      } else {
        this.Dices = [this.arrayXiu[0], this.arrayXiu[1], this.arrayXiu[2]];
        this.KQ = "xiu";
        console.log("xiu thang");
      }
    },

    xlTangLuot(e) {
      if (e === "choilai") {
        this.LuotChoi1++;
      } else {
        this.LuotNap++;
      }
    },
    xlAdminBuff(e, id) {
      let doiSangNumber, doiSangNumber1;
      if (id === 2 || id === 5 || id === 6) {
        doiSangNumber1 = Number(e);
      } else {
        doiSangNumber = Number(e.replace(/\./g, ""));
      }

      if (id === 1) {
        this.TongTien = doiSangNumber;
        this.TongTienString = this.TongTien.toLocaleString("vi-VN", {});
      } else if (id === 2) {
        this.ThoiGianDuocSua = doiSangNumber1;
      } else if (id === 3) {
        this.BuffTienMin = doiSangNumber;
      } else if (id === 4) {
        this.BuffTienMax = doiSangNumber;
      } else if (id === 5) {
        this.LuotChoi1 = doiSangNumber1;
      } else if (id === 6) {
        this.LuotNap = doiSangNumber1;
      }
    },
    xlNapTien(e) {
      this.TongTien += e;
      this.TongTienString = this.TongTien.toLocaleString("vi-VN", {});
      this.openNap = !this.openNap;
      this.LuotNap--;
    },
    xlTongTienString() {
      let tien = Math.floor(Math.random() * (1500000 - 150000 + 1)) + 150000;
      this.TongTien = Number(tien);
      this.TongTienString = this.TongTien.toLocaleString("vi-VN", {});
    },
    xlHuy(e) {
      if (e === "huy") {
        this.TongTien += this.TienCuoc;
        this.TienCuoc = 0;
        this.DisabledCuoc = this.DisabledAll = false;
      } else if (e === "datcuoc") {
        this.TongTienString = this.TongTien.toLocaleString("vi-VN", {});

        this.DatCuoc = this.DisabledCuoc = true;
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
          if (this.DatCuoc === false) {
            this.TongTien += this.TienCuoc;
          }
          // console.log("het thoig gian");
          // console.log("tong tien: " + this.TongTien);
          // console.log("tiencuoc: " + this.TienCuoc);

          clearInterval(tg);
          this.TatHienThiThoiGian = !this.TatHienThiThoiGian;
          this.quayXucXac(this.ThoiGianQuayXucXac * 2);

          this.ThoiGian = ThoiGian2;
        }
      }, 1000);
      this.ArraySetInterval.push(tg);
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
      this.ArraySetInterval.push(count);

      startInterval(time);
    },

    quayXucXac(time) {
      let { ThoiGianQuayXucXac } = this;
      ThoiGianQuayXucXac = time;
      this.xlHetThoiGian();
      this.QuayBuffXucXac();

      let qxx = setInterval(() => {
        let d1 = Math.floor(Math.random() * 6) + 1;
        let d2 = Math.floor(Math.random() * 6) + 1;
        let d3 = Math.floor(Math.random() * 6) + 1;
        this.sumDices = d1 + d2 + d3;

        this.Dices = [d1, d2, d3];
        ThoiGianQuayXucXac--;
        if (ThoiGianQuayXucXac === 1) {
          clearInterval(qxx);
          console.log(" ");

          let congLaiTien = this.TongTien + this.TienCuoc;

          if (this.KieuHack === "thuong") {
            console.log("hack thuong");
            this.KetQuaQuay();
          } else if (this.KieuHack === "buff") {
            console.log("buff");
            console.log("tongtien: " + this.TongTien);

            if (congLaiTien >= 18000000) {
              console.log("congLaiTien: " + congLaiTien);
              if (this.TienCuoc >= 500000) {
                console.log("tienCuoc: 5k");

                this.xl28(this.xlBuffWin());
              } else if (this.TienCuoc >= 100000) {
                console.log("tienCuoc: 1k");

                this.xl46(this.xlBuffWin());
              } else if (this.TienCuoc === 0) {
                // trường hợp ng chơi k chọn cược gì.(quay thường)
                console.log("khong chon");
                this.KetQuaQuay();
              } else {
                console.log("tienCuoc: k");
                this.xl64(this.xlBuffWin());
              }
            } else if (congLaiTien >= 15000000) {
              console.log("congLaiTien: " + congLaiTien);
              if (this.TienCuoc >= 1000000) {
                console.log("tienCuoc: 1m");

                this.xl46(this.xlBuffWin());
              } else if (this.TienCuoc >= 500000) {
                console.log("tienCuoc: 5k");
                this.xl64(this.xlBuffWin());
              } else if (this.TienCuoc === 0) {
                // trường hợp ng chơi k chọn cược gì.(quay thường)
                console.log("khong chon");
                this.KetQuaQuay();
              } else {
                console.log("tienCuoc: k");
                this.xl82(this.xlBuffWin());
              }
            } else if (congLaiTien >= 10000000) {
              console.log("congLaiTien: " + congLaiTien);
              if (this.TienCuoc >= 1000000) {
                console.log("tienCuoc: 1m");
                this.xl55(this.xlBuffWin());
              } else if (this.TienCuoc >= 500000) {
                console.log("tienCuoc: 5k");
                this.xl73(this.xlBuffWin());
              } else if (this.TienCuoc === 0) {
                // trường hợp ng chơi k chọn cược gì.(quay thường)
                console.log("khong chon");
                this.KetQuaQuay();
              } else {
                console.log("tienCuoc: k");
                this.xl91(this.xlBuffWin());
              }
            } else {
              console.log("vao quay thuong cua buff");

              this.KetQuaQuay();
            }
          } else if (this.KieuHack === "10/0") {
            console.log("10/0");
            if (this.TienCuoc > 0) {
              console.log("da cuoc");
              this.xl100();
            } else {
              console.log("khong cuoc");
              this.KetQuaQuay();
            }
            console.log(" ");
          } else if (this.KieuHack === "7/3") {
            console.log("7/3");
            if (this.TienCuoc > 0) {
              this.xl73(this.xlBuffWin());
            } else {
              this.KetQuaQuay();
            }
          } else if (this.KieuHack === "3/7") {
            console.log("3/7");
            if (this.TienCuoc > 0) {
              this.xl37(this.xlBuffWin());
            } else {
              this.KetQuaQuay();
            }
          } else {
            console.log("0/10");
            if (this.TienCuoc > 0) {
              this.xl010();
              console.log("xl010");
            } else {
              this.KetQuaQuay();
              console.log("thuong");
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
          this.ArraySetInterval.push(doTre);
        }
      }, 500);
      this.ArraySetInterval.push(qxx);
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
          if (this.ThoiGianDuocSua != null) {
            this.ThoiGian = this.ThoiGianDuocSua;
          }

          this.arrayTai = [];
          this.arrayXiu = [];
          this.DatCuoc = false;
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
      this.ArraySetInterval.push(tgvm);
    },

    xlLuatChoi() {
      this.openLuatChoi = !this.openLuatChoi;
    },
    xlBatDau() {
      this.BatDau = true;
      this.HienThiTongTien = true;
      this.xlTongTienString();
      this.xlThoiGian();
    },
    xlChoiLai() {
      this.openChoiLai = !this.openChoiLai;
    },
    xlNap() {
      this.openNap = !this.openNap;
    },
    xlRutTien() {
      this.openRutTien = !this.openRutTien;
    },
    xlAdmin() {
      this.openAdmin = !this.openAdmin;
    },

    xlReset() {
      this.LuotChoi1--;

      this.ArraySetInterval.forEach((id) => {
        clearInterval(id);
      });
      this.ArraySetInterval = [];

      this.DatCuoc = false;
      this.arrayTai = [];
      this.arrayXiu = [];
      this.openChoiLai = false;
      this.DisabledAll = false;
      this.HienThiTienThuong = null;
      this.KQ = "";
      this.HienThiTienDaCuoc = [0, 0];
      this.DisabledCuoc = false;
      this.TienCuoc = 0;
      this.indexTenCuoc = [0, 0];
      this.HienThiFileButton = false;
      this.ScaleTongTien = [{ scale: false }, { scale: false }];
      this.HienThiTongTienCuoc = ["0", "0"];
      this.TongTienCuoc = [{ value: 0 }, { value: 0 }];
      this.SoNguoiChoi = [{ value: 0 }, { value: 0 }];
      this.TongTien = 300000;
      this.TongTienString = "600000";
      this.HienThiTongTien = false;
      this.HienThiThoiGianVanMoi = false;
      this.TatHienThiThoiGian = false;
      this.openLuatChoi = false;
      // this.BatDau = false;
      this.Dices = [3, 4, 6];
      this.ThoiGianVanMoi = 5;
      this.ThoiGianQuayXucXac = 5;
      this.ThoiGian = 10;
      this.BuffTienMin = 1000;
      this.BuffTienMax = 5000000;

      this.xlBatDau();
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
  width: 700px;
  left: 10%;
  margin-top: 3%;
  position: relative;
}
</style>
