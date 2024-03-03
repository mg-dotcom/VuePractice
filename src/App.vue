<!-- learn Life cycle and localstorage -->
<!-- <script>
export default {
  data() {
    return {
      toBlue: false,
    };
  },
  // beforeCreate Hook เข้าไปแก้ DOM โดยตรง
  beforeCreate() {
    console.log("beforeCreate");
  }, 
  // ดึง data ได้
  created() {
    console.log("created");
  },
  //DOM ยังไม่ถูกสร้าง แต่จะมาในเร็วๆนี้
  beforeMount() {
    console.log("beforeMount");
  },
  // DOM ถูกสร้างเสร็จแล้ว เราสามารถ เข้าถึง Element ต่างๆใน DOM ได้ทั้งหมด เช่นการ ดึงข้อมูลจาก input เป็นต้น
  mounted() {
    console.log("mounted");
  },
 // ----------------------------------
  beforeUpdate() {
    console.log("beforeUpdate");
  },
  //ในทุกๆครั้งที่มีการกดปุ่ม และ Elements ใน DOM มีการเปลี่ยนแปลง จะทำให้ updated hook ทำงาน
  updated() {
    console.log("updated");
  }, -->

<script>
export default {
  data() {
    return {
      toBlue: localStorage.getItem("toBlue") === "true" ? true : false,
    };
  },
  methods: {
    changeBg() {
      this.toBlue = !this.toBlue;
      localStorage.setItem("toBlue", this.toBlue);
    },
  },
};
</script>

<template>
  <div class="min-h-screen w-full" :class="{ 'bg-blue-400': toBlue }">
    <h2>Hello World</h2>
    <button class="bg-red-600" @click="changeBg">Click me</button>
  </div>
</template>

<style></style>
