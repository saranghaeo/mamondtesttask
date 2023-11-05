<template>
  <div>
    <label class="container">
      <input type="checkbox" v-model="Agreement" required />
      <span class="checkmark"></span>
    </label>
  </div>
</template>

<script>
export default {
  data() {
    return {
      Agreement: true,
    };
  },
};
</script>

<style scoped>
.container {
  display: block;
  position: relative;
  padding-left: 35px;
  margin-bottom: 12px;
  cursor: pointer;
  font-size: 22px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.container input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

.checkmark {
  position: absolute;
  top: 0;
  left: 0;
  height: 17px;
  width: 19px;
  background-color: #eee;
  border-radius: 5px;
}

.container:hover input ~ .checkmark {
  background-color: #ccc;
}

.container input:checked ~ .checkmark {
  background-color: #3586ff;
}

.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

.container input:checked ~ .checkmark:after {
  display: block;
}

.container .checkmark:after {
  background-image: "/src/assets/vector.svg";
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}
</style>
