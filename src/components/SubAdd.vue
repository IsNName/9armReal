<template>
  <div class="card display-3">
    <div class="card-body">
      <form @submit.prevent="handleSubmit()">
        <div class="row">
          <div class="col-lg-4 col-md-4 col-sm-6 mt-2">
            <label for="stdId" class="form-label">รหัสวิชา</label>
            <input
              type="text"
              id="stdId"
              class="form-control"
              v-model.trim="sub.id"
            />
          </div>
          <div class="col-lg-8 col-md-8 col-sm-6 mt-2">
            <label for="stdName" class="form-label">ชื่อวิชา</label>
            <input
              type="text"
              id="stdName"
              class="form-control"
              v-model.trim="sub.name"
            />
          </div>
          <div class="col-lg-2 col-md-3 col-sm-4 mt-2">
            <label for="subgrade" class="form-label">เกรด</label>
            <select
              id="subgrade"
              class="form-select form-control"
              v-model="sub.grade"
            >
              <option value="A">A</option>
              <option value="B+">B+</option>
              <option value="B">B</option>
              <option value="C+">C+</option>
              <option value="C">C</option>
              <option value="D+">D+</option>
              <option value="D">D</option>
              <option value="F">F</option>
              <option value="W">W</option>
            </select>
          </div>
          <div class="col-lg-2 col-md-3 col-sm-4 mt-2">
            <label for="subCre" class="form-label">หน่วยกิต</label>
            <select
              id="subCre"
              class="form-select form-control"
              v-model="sub.credit"
            >
              <option value="1">1</option>
              <option value="2">2</option>
              <option value="3">3</option>
              <option value="4">4</option>
            </select>
          </div>
          <div class="col-2 mt-4 d-flex align-item-center">
            <button
              id="btnSubmit"
              type="submit"
              class="btn btn-primary button-36"
            >
              <h1>บันทึก</h1>
            </button>
          </div>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "SubAdd",
  data() {
    return {
      sub: [],
    };
  },
  methods: {
    handleSubmit() {
      let subject = {
        id: this.sub.id,
        name: this.sub.name,
        grade: this.sub.grade,
        credit: this.sub.credit,
        isShow: false,
      };
      fetch("http://localhost:3000/subject", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(subject),
      })
        .then(() => {
          this.addSuccess = true;
          alert("บันทึกข้อมูลเรียบร้อยแล้ว");
          location.reload();
        })
        .catch((err) => {
          this.addError = true;
          this.errMessage = err;
        });
    },
  },
};
</script>

<style>
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
.form-control {
  width: 100%; /* กำหนดความกว้างให้เต็มหน้าจอ */
  height: 70px; /* กำหนดความสูงของช่อง input */
  font-size: 26px; /* กำหนดขนาดตัวอักษร */
  /* เพิ่มคุณสมบัติอื่น ๆ ตามต้องการ */
}
</style>