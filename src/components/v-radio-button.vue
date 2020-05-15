<template>
  <label class="button-radio">
    <span
      class="button-span"
      :class="[{'isActive': label == data.value}, 
      {'disabled': disabled || data.disabled}, 
      [data.size]]"
      :style="label == data.value ? activeStyle:null"
    >{{label}}</span>
    <input 
    type="radio" 
    :name="name" 
    :disabled="disabled || data.disabled" 
    @click="change" />
  </label>
</template>
<script>
//import bus from '../assets/event.js';
export default {
  name: "VradioButton",
  props: {
    label: {},
    name: {
      type: String
    },
    disabled: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      data: this.$parent
    };
  },
  computed: {
    activeStyle: function() {
      return {
        backgroundColor: this.data.fill,
        color: this.data.textColor,
        borderColor: this.data.fill
      };
    }
  },
  methods: {
    change: function() {
      this.$emit("input", this.label);
    }
  }
};
</script>
<style scoped lang="stylus">
.button-radio {
  position: relative;
}

input {
  position: absolute;
  opacity: 0;
  top: 0;
  left: 0;
}

.button-span {
  display: inline-block;
  font-size: $fontSize;
  padding: 12px 20px;
  background: $mainBackgroundColor;
  color: $mainTextColor;
  border: 1px solid $mainBorderColor;
  cursor: pointer;
  border-left: 0;
}

.button-span:hover {
  color: $mainColor;
}

.small {
  padding: 10px 20px;
}

.mini {
  padding: 9px 15px;
}

.disabled {
  color: $disabledColor;
  cursor: not-allowed;
  background-color: $mainBackgroundColor;
  border-color: $disabledBorderColor;
}

.disabled:hover {
  color: $disabledColor;
}

.disabled.isActive {
  background-color: #f2f6fc !important;
  color: $disabledColor !important;
  border-color: $disabledBorderColor !important;
}
</style>