<template>
  <div class="LuatChoi" :class="{ on: this.openLuatChoi }">
    <div class="lc">
      <h3>Luật Chơi</h3>
      <p>
        Với tài xỉu, bạn sử dụng 3 viên xúc xắc (hay còn gọi là xí ngầu). Mỗi
        viên xúc xắc có 6 mặt và người chơi sẽ đặt cược kết quả sau khi nhà cái
        lắc xúc xắc. Nếu kết quả trên tổng 3 mặt của xúc xắc là 3 đến 10 thì đó
        gọi là “Xỉu”, còn nếu là 11 đến 18 thì đó là “Tài”.
      </p>
      <h3>Chơi Lại</h3>
      <p>
        Người chơi chỉ có duy nhất 1 lượt chơi lại, lượt chơi lại sẽ được cộng
        thêm 1 lượt sau mỗi 15 phút.
      </p>
      <h3>Admin</h3>
      <p>
        Chỉ có Admin được phép truy cập vào mục này.
        <strong> Liên hệ: TaT</strong>.
      </p>
      <h3>Nạp Tiền</h3>
      <p>
        Người chơi sẽ có 2 lần nạp. Mỗi lần nạp tối đa là 500k. Thời gian nạp sẽ
        tăng lên 1 lượt sau mỗi 10 phút.
      </p>
      <h3>Rút Tiền</h3>
      <p>
        Đảm bảo rằng, tổng số tiền của bạn phải từ
        <strong>20 triệu</strong> trở lên.
      </p>
      <button @click="thoat">Thoát</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "LuatChoi",
  props: {
    openLuatChoi: { type: Boolean, default: false },
  },
  methods: {
    thoat() {
      this.$emit("xlLuatChoi");
    },
  },
};
</script>

<style>
:root {
  --mauHover: rgb(37, 37, 186);
  --mauLinear: linear-gradient(to bottom, #0000ff, #87ceeb);
}
.LuatChoi {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.4);
  opacity: 0;
  visibility: hidden; /*ẩn fome luật chơi k bị trễ*/
  transition: all 0.5s ease;
}
.LuatChoi.on {
  visibility: visible;
  opacity: 1;
}

.lc {
  width: 700px;
  padding: 0 10px;
  top: 30%;
  left: 50%;
  transform: translate(-50%, -30%) scale(1.2);
  background: rgb(241, 244, 246);
  position: absolute;
  transition: all 0.5s ease;
  border: 3px double #0000ff;
  border-radius: 15px;
}
.on .lc {
  transform: translate(-50%, -30%) scale(1);
}
.lc h3 {
  padding: 15px 0 0 0;
  color: #0000ffa5;
}

.lc button {
  padding: 5px 20px;
  margin: 10px;
  border-radius: 10px;
  background: var(--mauLinear);
  color: white;
  border: 1px solid white;
  cursor: pointer;
}
.lc button:hover {
  background: var(--mauHover);
}
</style>
