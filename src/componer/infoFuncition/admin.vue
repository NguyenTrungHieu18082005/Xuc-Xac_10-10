<template>
  <div class="Admin" :class="{ on: openAdmin }">
    <div class="DangNhap" :class="{ on: HienThiDangNhap }">
      <div class="wrapper">
        <div class="flip-card__front">
          <div class="title">Log in</div>
          <form class="flip-card__form" type="button">
            <input
              class="flip-card__input"
              name="email"
              placeholder="Name"
              type="text"
              v-model="Name"
            />
            <input
              class="flip-card__input"
              name="password"
              placeholder="Password"
              type="password"
              v-model="Pass"
            />
            <div class="buttonLogin">
              <button class="flip-card__btn" type="button" @click="login">
                Login
              </button>
              <button class="flip-card__btn" type="button" @click="exit">
                Exit
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>

    <!-- id của radio dùng để liên kết tới label hiển thị radio đó, khi ấb vào label thì sẽ radio đó được chọn -->
    <div class="admin" :class="{ on: HienThiAdmin }">
      <div class="buffThangThua">
        <div>
          <input
            type="radio"
            name="a"
            id="option1"
            value="thuong"
            v-model="KieuHack1"
          />
          <label for="option1">Thường</label>
        </div>

        <div>
          <input
            type="radio"
            name="a"
            id="option2"
            checked
            value="buff"
            v-model="KieuHack1"
          />
          <label for="option2">Buff</label>
        </div>

        <div>
          <input
            type="radio"
            name="a"
            id="option3"
            value="10/0"
            v-model="KieuHack1"
          />
          <label for="option3">10/0</label>
        </div>

        <div>
          <input
            type="radio"
            name="a"
            id="option4"
            value="7/3"
            v-model="KieuHack1"
          />
          <label for="option4">7/3</label>
        </div>

        <div>
          <input
            type="radio"
            name="a"
            id="option5"
            value="3/7"
            v-model="KieuHack1"
          />
          <label for="option5">3/7</label>
        </div>

        <div>
          <input
            type="radio"
            name="a"
            id="option6"
            value="0/10"
            v-model="KieuHack1"
          />
          <label for="option6">0/10</label>
        </div>
      </div>

      <div class="buff">
        <div>
          <label for="buffTien">Buff Tien</label>
          <input
            type="text"
            id="buffTien"
            v-model="BuffTien"
            @input="chuyendoiSo(1)"
          />
        </div>

        <div>
          <label for="thoiGian">Thoi Gian</label>
          <input
            type="text"
            id="thoiGian"
            v-model="ThoiGian"
            @input="chuyendoiSo(2)"
          />
        </div>

        <div>
          <label for="buffMin">Buff Min</label>
          <input
            type="text"
            id="buffMin"
            v-model="BuffMin"
            @input="chuyendoiSo(3)"
          />
        </div>

        <div>
          <label for="buffMax">Buff Max</label>
          <input
            type="text"
            id="buffMax"
            v-model="BuffMax"
            @input="chuyendoiSo(4)"
          />
        </div>

        <div>
          <label for="luotChoi">Luot Choi</label>
          <input
            type="text"
            id="luotChoi"
            v-model="LuotChoi"
            @input="chuyendoiSo(5)"
          />
        </div>

        <div>
          <label for="napTien">Nap Tien</label>
          <input
            type="text"
            id="napTien"
            v-model="NapTien"
            @input="chuyendoiSo(6)"
          />
        </div>
      </div>

      <button @click="auke">Ấu Kề</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Admin",
  data() {
    return {
      KieuHack1: "buff",

      BuffTien: "",
      ThoiGian: "",
      BuffMin: "",
      BuffMax: "",
      LuotChoi: "",
      NapTien: "",
      HienThiAdmin: false,
      Name: "",
      Pass: "",

      ThangThua: ["Thường", "Buff", "10/0", "7/3", "3/7", "0/10"],
    };
  },

  props: {
    openAdmin: { type: Boolean, default: false },
  },
  computed: {
    HienThiDangNhap() {
      if (this.openAdmin && this.HienThiAdmin === false) {
        return true;
      }
      return false;
    },
  },
  methods: {
    hack() {},

    exit() {
      this.$emit("xlAdmin");
      this.Name = this.Pass = "";
    },
    chuyendoiSo(e) {
      if (e === 1) {
        let value = this.BuffTien.replace(/[^0-9]/g, "");
        this.BuffTien = Number(value).toLocaleString("de-DE");
      } else if (e === 2) {
        this.ThoiGian = Number(this.ThoiGian.replace(/[^0-9]/g, ""));
      } else if (e === 3) {
        let value = this.BuffMin.replace(/[^0-9]/g, "");
        this.BuffMin = Number(value).toLocaleString("de-DE");
      } else if (e === 4) {
        let value = this.BuffMax.replace(/[^0-9]/g, "");
        this.BuffMax = Number(value).toLocaleString("de-DE");
      } else if (e === 5) {
        this.LuotChoi = Number(this.LuotChoi.replace(/[^0-9]/g, ""));
      } else {
        let value = this.NapTien.replace(/[^0-9]/g, "");
        this.NapTien = Number(value).toLocaleString("de-DE");
      }
    },
    auke() {
      this.$emit("xlKieuHack", this.KieuHack1);

      this.HienThiAdmin = !this.HienThiAdmin;
      this.$emit("xlAdmin");
      this.Name = this.Pass = "";

      if (this.BuffTien != "0" && this.BuffTien != "") {
        this.$emit("xlAdminBuff", this.BuffTien, 1);
      }
      if (this.ThoiGian != "0" && this.ThoiGian != "") {
        this.$emit("xlAdminBuff", this.ThoiGian, 2);
      }
      if (this.BuffMin != "0" && this.BuffMin != "") {
        this.$emit("xlAdminBuff", this.BuffMin, 3);
      }
      if (this.BuffMax != "0" && this.BuffMax != "") {
        this.$emit("xlAdminBuff", this.BuffMax, 4);
      }
      if (this.LuotChoi != "0" && this.LuotChoi != "") {
        this.$emit("xlAdminBuff", this.LuotChoi, 5);
      }
      if (this.NapTien != "0" && this.NapTien != "") {
        this.$emit("xlAdminBuff", this.NapTien, 6);
      }
    },
    login() {
      if (this.Name === "admin" && this.Pass === "1231") {
        this.HienThiAdmin = !this.HienThiAdmin;
      } else if (this.name === "" || this.Pass === "") {
        alert("Vui lòng điền đủ thông tin.");
      } else {
        alert("Đã xảy ra sự cố, vui lòng quay lại sau.");
      }
    },
  },
};
</script>

<style>
.Admin {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #6ca7ff80;
  transition: all 0.5s ease;

  opacity: 0;
  visibility: hidden;
}
.Admin.on {
  opacity: 1;
  visibility: visible;
}
.DangNhap {
  position: absolute;
  top: 20%;
  right: 0%;
  transition: all 0.5s ease;

  opacity: 0;
  visibility: hidden;
}
.DangNhap.on {
  opacity: 1;
  visibility: visible;

  right: 70%;
}

.Admin .admin {
  position: absolute;
  top: 40%;
  left: 40%;
  transform: translate(-40%, -40%);
  border: 3px solid transparent;
  background-color: rgb(255, 255, 255);
  padding: 10px;
  gap: 10px;
  border-radius: 10px;
  box-shadow: 4px 4px rgba(23, 23, 23, 0.646);

  animation: moveBorder 4s linear infinite;

  display: flex;
  opacity: 0;
  visibility: hidden;
}
.Admin .admin.on {
  opacity: 1;
  visibility: visible;
}
@keyframes moveBorder {
  0% {
    border-top-color: blue;
  }
  25% {
    border-right-color: blue;
  }
  50% {
    border-bottom-color: blue;
    box-shadow: 4px 4px rgba(0, 0, 255, 0.625);
  }
  75% {
    border-left-color: blue;
  }
  100% {
    border-top-color: transparent;
  }
}

.buffThangThua,
.buff {
  width: 250px;
  border-radius: 5px;
  border: 1px solid #000000;
  padding: 10px;
  line-height: 1.5;
  box-shadow: 4px 4px rgba(23, 23, 23, 0.485);
  font-weight: bold;
}
.buffThangThua {
  width: 100px;
}

.buffThangThua div,
.buff div {
  margin-bottom: 5px;
}
.buffThangThua input,
.buffThangThua label {
  cursor: pointer;
}

.admin .buff input {
  font-weight: bold;
  width: 150px;
}
.buffThangThua:hover,
.buff:hover {
  animation: moveBorder 3s linear infinite;
  border: 1px solid transparent;
}

.buffThangThua div:hover {
  color: blue;

  animation: moveBorder 2s linear infinite;
  border: 1px solid transparent;
  border-radius: 10px;
}

.admin .buffInput {
  width: 100px;
  font-weight: bold;
}
.admin button {
  padding: 0 10px;
  border-radius: 7px;
  font-weight: bold;
  background-color: rgb(255, 255, 255);
}
.admin button:hover {
  animation: moveBorder 3s linear infinite;

  border: 2px solid transparent;
  background-color: rgba(198, 220, 228, 0.767);
  cursor: pointer;
}

.wrapper {
  --font-color: #323232;
  --font-color-sub: #666;
  --bg-color: #fff;
  --bg-color-alt: #666;
  --main-color: #323232;
}

.flip-card__front,
.flip-card__back {
  padding: 20px;
  position: absolute;
  display: flex;
  flex-direction: column;
  justify-content: center;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
  background: lightgrey;
  gap: 20px;
  border-radius: 5px;
  border: 2px solid var(--main-color);
  box-shadow: 4px 4px var(--main-color);
}

.flip-card__form {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
}

.flip-card__input {
  width: 250px;
  height: 40px;
  border-radius: 5px;
  border: 2px solid var(--main-color);
  background-color: var(--bg-color);
  box-shadow: 4px 4px var(--main-color);
  font-size: 15px;
  font-weight: 600;
  color: var(--font-color);
  padding: 5px 10px;
  outline: none;
}

.flip-card__btn {
  margin: 20px 0 20px 0;
  width: 120px;
  height: 40px;
  border-radius: 5px;
  border: 2px solid var(--main-color);
  background-color: var(--bg-color);
  box-shadow: 4px 4px var(--main-color);
  font-size: 17px;
  font-weight: 600;
  color: var(--font-color);
  cursor: pointer;
  margin-left: 3px;
}

.flip-card__btn:active {
  box-shadow: 0px 0px var(--main-color);
  transform: translate(3px, 3px);
}
</style>
