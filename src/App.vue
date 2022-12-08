<template>
  <student />
  <show-student />
  <button @click="buttons">hahaha</button>
</template>

<script>
// import HelloWorld from "./components/HelloWorld.vue";
// import StudenManagmentVue from "./components/StudenManagment.vue";
import ShowStudentVue from "./components/ShowStudent.vue";
export default {
  name: "App",
  components: {
    // HelloWorld,
    // Student: StudenManagmentVue,
    ShowStudent: ShowStudentVue,
  },

  data() {
    return {};
  },
  methods: {
    buttons() {},
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  /* height: 1000px; */
}
body {
  height: 1000px;
}
</style>
