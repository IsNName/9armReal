<template>
  <div class="m-5">
    <div class="float-start m-1">
      <h1 class="display-3 iridescent-text">PORTFOLIO</h1>

      <div class="text-center">
        <div class="m-5">
          <div class="float-start m-5 iridescent-border">
            <img src="./assets/wasawat.jpg" alt="" width="300" />
          </div>
        </div>
      </div>
      <h1 class="display-5">{{ name }}</h1>
      <h5 class="text-danger">{{ des }}</h5>
      <h5 class="text-danger">{{ hobbies }}</h5>
      <div class="display-2">
        <button class="button-36" role="button" @click="toggleList()">
          <h1>เเสดงผลการเรียน</h1>
        </button>

        <div>
          <button class="button-36" role="button" @click="toggleAdd()">
            <h1>เพิ่มผลการเรียน</h1>
          </button>
        </div>
      </div>
    </div>
  </div>
  <div class="text-center">
    <div class="m-2" v-if="showSubEdit">
      <SubEdit :stdId="someIdHere" />
    </div>
    <div class="float-center">
      <div class="m-2" v-if="showSubAdd">
        <SubAdd />
      </div>
    </div>
    <div class="text-center">
      <div class="m-2" v-if="showSubList">
        <SubList :students="students" />
      </div>
    </div>
  </div>
</template>

<script>
import SubAdd from "./components/SubAdd";
import SubList from "./components/SubList";

export default {
  name: "App",
  components: {
    SubList,
    SubAdd,
  },
  data() {
    return {
      name: "",
      major: "",
      des: "",
      hobbies: "",
      image: "",
      showSubList: false,
      showSubAdd: false,
      showSubEdit: false,
      students: [],
      someIdHere: 123,
    };
  },
  mounted() {
    fetch("http://localhost:3000/Data_me")
      .then((res) => res.json())
      .then((data) => {
        if (Array.isArray(data) && data.length > 0) {
          const student = data[0];
          this.name = student.name || "ไม่พบข้อมูล";
          this.des = student.des || "ไม่พบข้อมูล";
          this.hobbies = student.hobbies || "ไม่พบข้อมูล";
          this.image = student.image || "ไม่พบข้อมูล";
          this.students = data;
        } else {
          this.name = "ไม่พบข้อมูล";
          this.gra = "ไม่พบข้อมูล";
          this.des = "ไม่พบข้อมูล";
        }
      })
      .catch((err) => console.log(err.message));
  },
  methods: {
    toggleList() {
      this.showSubList = !this.showSubList;
      this.showSubAdd = false;
      this.showSubEdit = false;
    },
    toggleAdd() {
      this.showSubAdd = !this.showSubAdd;
      this.showSubList = false;
      this.showSubEdit = false;
    },
    toggleEdit() {
      this.showSubEdit = !this.showSubEdit;
      this.showSubList = false;
      this.showSubAdd = false;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
@keyframes rainbow {
  0% {
    color: red;
  }
  16% {
    color: orange;
  }
  33% {
    color: yellow;
  }
  50% {
    color: green;
  }
  66% {
    color: blue;
  }
  83% {
    color: indigo;
  }
  100% {
    color: violet;
  }
}

.rainbow-text {
  animation: rainbow 4s infinite;
  background: linear-gradient(
    to right,
    red,
    orange,
    yellow,
    green,
    blue,
    indigo,
    violet
  );
  background-clip: text;
  -webkit-background-clip: text;
  color: transparent;
}
@keyframes iridescent {
  0% {
    color: #ff00ff;
  }
  10% {
    color: #ff00ff;
  }
  20% {
    color: #00ffff;
  }
  30% {
    color: #00ff00;
  }
  40% {
    color: #ffff00;
  }
  50% {
    color: #ff0000;
  }
  60% {
    color: #0000ff;
  }
  70% {
    color: #ff0000;
  }
  80% {
    color: #ffff00;
  }
  90% {
    color: #00ff00;
  }
  100% {
    color: #00ffff;
  }
}
.iridescent-text {
  animation: iridescent 5s infinite;
}
/* CSS สำหรับสร้างกรอบรูปที่มีสีรุ้ง */
/* CSS สำหรับสร้างกรอบรูปที่มีลักษณะเรืองแสง */
.iridescent-border {
  border-radius: 10px; /* ปรับความโค้งของเส้นขอบตามต้องการ */
  border: 10px solid transparent; /* ตั้งค่าเส้นขอบให้เป็นโปร่งๆ */
  background: linear-gradient(
    to right,
    #ff00ff,
    #00ff00,
    #ffff00,
    #ff0000,
    #0000ff
  ); /* Gradient Background สีเรืองแสง */
  background-clip: padding-box; /* ให้สีเรืองแสงเฉพาะพื้นที่ที่เป็น background ของ div */
  animation: iridescent-border 5s infinite; /* สร้าง Animation สำหรับการเปลี่ยนแปลงสีเรืองแสง */
  display: flex;
  justify-content: flex-start; /* จัดตำแหน่งซ้าย */
  align-items: center;
}

/* สร้าง Animation เพื่อเปลี่ยนแปลงสีเรืองแสงในกรอบ */
@keyframes iridescent-border {
  0% {
    border-color: #ff00ff;
  }
  25% {
    border-color: #00ff00;
  }
  50% {
    border-color: #ffff00;
  }
  75% {
    border-color: #ff0000;
  }
  100% {
    border-color: #0000ff;
  }
}
.button-36 {
  background-image: linear-gradient(
    92.88deg,
    #455eb5 9.16%,
    #5643cc 43.89%,
    #673fd7 64.72%
  );
  border-radius: 8px;
  border-style: none;
  box-sizing: border-box;
  color: #ffffff;
  cursor: pointer;
  flex-shrink: 0;
  font-family: "Inter UI", "SF Pro Display", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue",
    sans-serif;
  font-size: 16px;
  font-weight: 500;
  height: 4rem;
  padding: 0 1.6rem;
  text-align: center;
  text-shadow: rgba(0, 0, 0, 0.25) 0 3px 8px;
  transition: all 0.5s;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  animation: rainbow 10s linear infinite;
}

@keyframes rainbow {
  0% {
    background-position: 0% 50%;
  }
  100% {
    background-position: 100% 50%;
  }
}

.button-36:hover {
  box-shadow: rgba(80, 63, 205, 0.5) 0 1px 30px;
  transition-duration: 0.1s;
}

@media (min-width: 768px) {
  .button-36 {
    padding: 0 2.6rem;
  }
}
</style>