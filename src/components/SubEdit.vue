<template>
  <div>
    <h2>แก้ไขรายวิชา</h2>
    <form @submit.prevent="handleSubmit">
      <div class="mb-3">
        <label for="editId" class="form-label">รหัสวิชา</label>
        <input
          type="text"
          class="form-control"
          id="editId"
          v-model="editedStudent.id"
        />
      </div>
      <div class="mb-3">
        <label for="editName" class="form-label">ชื่อวิชา</label>
        <input
          type="text"
          class="form-control"
          id="editName"
          v-model="editedStudent.name"
        />
      </div>
      <div class="mb-3">
        <label for="editMajor" class="form-label">เกรด</label>
        <input
          type="text"
          class="form-control"
          id="editMajor"
          v-model="editedStudent.grade"
        />
      </div>
      <div class="mb-3">
        <label for="editYear" class="form-label">หน่วยกิต</label>
        <input
          type="number"
          class="form-control"
          id="editYear"
          v-model="editedStudent.credit"
        />
      </div>

      <button type="submit" class="btn btn-primary display-5 butt button-36">
        <h3>บันทึกการแก้ไข</h3>
      </button>
    </form>
  </div>
</template>

<script>
export default {
  name: "SubEdit",
  props: ["stdId"],
  data() {
    return {
      editedStudent: [],
    };
  },
  mounted() {
    this.fetchStudentData();
  },
  methods: {
    fetchStudentData() {
      fetch(`http://localhost:3000/subject/${this.stdId}`)
        .then((response) => response.json())
        .then((data) => {
          this.editedStudent = data;
        })
        .catch((error) => {
          console.error("Error fetching student data:", error);
        });
    },
    handleSubmit() {
      fetch(`http://localhost:3000/subject/${this.stdId}`, {
        method: "PUT",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(this.editedStudent),
      })
        .then(() => {
          alert("บันทึกการแก้ไขข้อมูลเรียบร้อยแล้ว");
          location.reload();
        })
        .catch((error) => {
          console.error("Error updating student data:", error);
          alert("เกิดข้อผิดพลาดในการบันทึกการแก้ไขข้อมูล");
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