<template>
  <div>
    <div class="card my-2">
      <div class="card-body bg-info bg-opacity-10">
        <h3 class="card-title">รหัสวิชา {{ subject.id }}</h3>
        <div class="card-sub-title">ชื่อวิชา {{ subject.name }}</div>
        <div class="cart-text">
          เกรดวิชา {{ subject.grade }} หน่วยกิต {{ subject.credit }}
        </div>
      </div>
    </div>
    <button class="btn btn-success button-36" @click="editDetail">
      <h3>แก้ไขข้อมูล</h3>
    </button>
    &nbsp;
    <button class="btn btn-success button-36" @click="delDetail(stdId)">
      <h3>ลบข้อมูล</h3>
    </button>
    <!-- เพิ่มส่วนนี้เพื่อเรียกใช้ SubEdit.vue -->
    <div v-if="isEdit">
      <SubEdit :stdId="stdId" />
    </div>
  </div>
</template>

<script>
import SubEdit from "./SubEdit.vue"; // Import SubEdit component

export default {
  name: "SubDetail",
  props: ["stdId"],
  data() {
    return {
      subject: [],
      isEdit: false,
    };
  },
  mounted() {
    this.fetchStudentData();
  },
  methods: {
    fetchStudentData() {
      fetch(`http://localhost:3000/subject/${this.stdId}`)
        .then((res) => res.json())
        .then((data) => (this.subject = data))
        .catch((err) => console.log(err.message));
    },
    editDetail() {
      this.isEdit = !this.isEdit;
    },
    delDetail(theId) {
      fetch("http://localhost:3000/subject/" + theId, {
        method: "DELETE",
      })
        // ส่งสัญญาณไปบอก Component ที่เรียกว่า Delete แล้ว
        .then(this.$emit("delete"))
        .catch((err) => console.log(err.message));
    },
  },
  components: {
    SubEdit, // Register SubEdit component
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
</style>