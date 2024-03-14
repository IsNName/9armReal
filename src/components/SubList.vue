<template>
  <h1>ผลการเรียน</h1>
  <ul class="list-group">
    <li
      v-for="(std, id) in subject"
      :key="id"
      class="list-group-item list-group-item-light display-5"
    >
      <a
        href="#"
        class="list-group-item list-group-item-action display-5"
        @click="setShow(std)"
      >
        {{ std.name }}
      </a>
      <div v-if="std.isShow">
        <SubDetail :stdId="std.id" @edit="showEdit" @delete="reload()" />
      </div>
    </li>
    <div v-if="isEdit">
      {{ EditId }}
    </div>
  </ul>

  <br /><br />
</template>

<script>
import SubDetail from "./SubDetail.vue";

export default {
  name: "SubList",
  components: {
    SubDetail,
  },
  data() {
    return {
      subject: [],
      isEdit: false,
      EditId: "",
    };
  },
  mounted() {
    fetch("http://localhost:3000/subject")
      .then((res) => res.json())
      .then((data) => (this.subject = data))
      .catch((err) => console.log(err.message));
  },
  methods: {
    setShow(theId) {
      theId.isShow = !theId.isShow;
    },
    showEdit(theStdId) {
      this.EditId = theStdId;
      this.isEdit = true;
    },
    reload() {
      this.$parent.showSubList = !this.$parent.showSubList;
    },
  },
};
</script>

<style>
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
</style>