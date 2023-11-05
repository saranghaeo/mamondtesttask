<template>
  <div>
    <label class="switch">
      <input type="checkbox" 
      :checked="isPublic" 
      @change="updateIsPublic" />
      <span class="slider"></span>
    </label>
  </div>
</template>

<script>
export default {
  props: {
    isPublic: Boolean,
  },
  methods: {
    updateIsPublic() {
      this.$emit("update:isPublic", !this.isPublic);
    },
  },
};
</script>

<style scoped>
* {
  background: none;
}
.switch {
  position: relative;
  display: inline-block;
  width: 39px;
  height: 19px;
}

.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #f5f6f8;
  -webkit-transition: 0.4s;
  transition: 0.4s;
  border-radius: 100px;
}

.slider:before {
  position: absolute;
  content: "";
  height: 19px;
  width: 19px;
  background-color: white;
  -webkit-transition: 0.4s;
  transition: 0.4s;
  border-radius: 100px;
}

input:checked + .slider {
  background-color: #3586ff;
}

input + .slider {
  box-shadow: 0 0 2px #3586ff;
}

input:checked + .slider:before {
  -webkit-transform: translateX(20px);
  -ms-transform: translateX(20px);
  transform: translateX(20px);
}
</style>
