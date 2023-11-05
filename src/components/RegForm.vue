<template>
  <form class="container-reg-form" @submit.prevent="submit">
    <div class="title">
      <h2>Регистрация</h2>
      <DividingLine />
    </div>

    <div class="main-section-reg-form">
      <h3>Заполните Ваши данные</h3>

      <div class="inputs">
        <input
          type="text"
          placeholder="Имя"
          v-model="name"
          style="margin-right: 10px"
          required
        />
        <input type="email" placeholder="Email" v-model="email" required />
      </div>

      <div class="selects">
        <select v-model="selected">
          <option :value="1">Вариант 1</option>
          <option :value="2">Вариант 2</option>
          <option :value="3">Вариант 3</option>
        </select>
      </div>

      <div class="inputs">
        <input
          type="password"
          placeholder="Пароль"
          v-model="password"
          style="margin-right: 10px"
          required
        />
        <input
          type="password"
          placeholder="Повторить пароль"
          v-model="password_repeat"
          required
        />
      </div>

      <span v-if="password !== password_repeat">Пароли не совпадают.</span>
    </div>

    <DividingLine />

    <div class="checkbox-reg-btn">
      <div class="switcher">
        <SwitcherComp :isPublic="isPublic" @update:isPublic="updateIsPublic" />
        <div class="text">
          <p>Хотите чтобы Ваш профиль видели другие участники платформы?</p>
          <p class="sub-text">
            Включает профиль для просмотра другими пользователями по ссылке
          </p>
        </div>
      </div>

      <div class="checkbox">
        <CheckboxComp required />
        <p class="license_agreement">
          Регистрируясь, Вы соглашаетесь с
          <a href="www">политикой конфиденциальности</a> и
          <a href="www">обработкой персональных данных</a>.
        </p>
        <button class="btn-reg" type="submit">Зарегистрироваться</button>
      </div>
    </div>
  </form>
</template>

<script>
import axios from "axios";
import DividingLine from "./ForRegistartionForm/DividingLine.vue";
import SwitcherComp from "./ForRegistartionForm/SwitcherComp.vue";
import CheckboxComp from "./ForRegistartionForm/CheckboxComp.vue";

export default {
  name: "app",
  components: {
    DividingLine,
    SwitcherComp,
    CheckboxComp,
  },
  data() {
    return {
      name: "",
      email: "",
      selected: "1",
      password: "",
      password_repeat: "",
      Agreement: true,
      isPublic: false,
      passwordMismatch: false,
    };
  },
  methods: {
    updateIsPublic(newValue) {
      this.isPublic = newValue;
    },
    submit() {
      if (this.password !== this.password_repeat) {
        this.passwordMismatch = true;
        return;
      }
      this.passwordMismatch = false;
      const data = {
        name: this.name,
        email: this.email,
        role: this.selected,
        password: this.password,
        password_repeat: this.password_repeat,
        public: this.isPublic,
      };
      axios
        .post("https://jsonplaceholder.typicode.com/posts", data)
        .then((response) => {
          console.log(response);
          this.$emit("registrationSuccess");
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>

<style scoped>
* {
  background: white;
}

a {
  text-decoration: none;
  color: #3586ff;
}

span {
  color: red;
  font-size: 14px;
  padding: 5px 10px;
}

.container-reg-form {
  width: 960px;
  border-radius: 15px;
  padding: 15px 0 20px 0;
}

.title h2 {
  font-size: 19px;
  font-weight: 700;
  padding: 10px 30px 0 30px;
}

.main-section-reg-form {
  padding: 20px 30px;
}

h3 {
  font-size: 16px;
  font-weight: 500;
  line-height: 19px;
}

.inputs {
  display: flex;
  padding: 15px 0px;
}

input {
  display: flex;
  width: 445px;
  height: 39px;
  padding: 10px;
  color: var(--grayscale-600, #9292a0);
  font-size: 14px;
  line-height: 19px; /* 135.714% */
  letter-spacing: -0.021px;
  background: #fff;
  border-radius: 11px;
  border: 1px solid var(--grayscale-300, #e6e6eb);
}

input:focus {
  color: #000;
  border-color: #929292;
}

.selects {
  display: flex;
  justify-content: flex-end;
}

select {
  display: flex;
  width: 445px;
  height: 39px;
  padding: 10px;
  color: var(--grayscale-600, #9292a0);
  font-size: 14px;
  line-height: 19px; /* 135.714% */
  letter-spacing: -0.021px;
  background: #fff;
  border-radius: 11px;
  border: 1px solid var(--grayscale-300, #e6e6eb);
}

select:focus {
  color: #000;
}

.checkbox-reg-btn {
  padding: 30px 30px 15px 30px;
}

.switcher {
  display: flex;
}

.text {
  padding-left: 5px;
  font-weight: 500;
}

.sub-text {
  padding-top: 10px;
  color: var(--grayscale-700, #696977);
  font-size: 14px;
  font-weight: 400;
  line-height: 19px; /* 135.714% */
  letter-spacing: -0.021px;
}

.checkbox {
  display: flex;
  padding-top: 30px;
}

.license_agreement {
  font-size: 14px;
}

.btn-reg {
  width: 302px;
  height: 40px;
  border-radius: 8px;
  background: rgba(73, 122, 218, 0.2);
  color: #497ada;
  font-family: Montserrat;
  line-height: 19px; /* 158.333% */
  letter-spacing: -0.018px;
}
</style>
