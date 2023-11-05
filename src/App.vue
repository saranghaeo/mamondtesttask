<template>
  <div id="app">
    <div v-if="!registrationSuccess">
      <RegForm @registrationSuccess="handleRegistrationSuccess" />
    </div>
    <div v-else>
      <p>Регистрация успешно завершена.</p>
    </div>
  </div>
</template>

<script>
import RegForm from "./components/RegForm.vue";

export default {
  name: "App",
  components: {
    RegForm,
  },
  data() {
    return {
      registrationSuccess: false,
      successMessage: "",
    };
  },
  methods: {
    handleRegistrationSuccess() {
      this.registrationSuccess = true;
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,400;0,700;1,500&display=swap");

*,
*::before,
*::after {
  padding: 0;
  margin: 0;
  border: 0;
  box-sizing: border-box;
  background: #ececec;
}

#app {
  font-family: Montserrat, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #000;
  margin: 60px;
}
</style>
