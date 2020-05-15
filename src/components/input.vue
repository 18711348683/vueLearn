<template>
  <div class="v-input">
    <input
      :class="[{'disabled': disabled}]"
      :value="value"
      :placeholder="placeholder"
      :disabled="disabled"
      :clearable="clearable"
      @input="input"
      @focus="focus"
      @mouseenter="mouseenter"
      @mouseleave="mouseleave"
      :maxlength="maxlength"
    />
    <span v-if="isClearable"  class="clearable">
      <i class="icon-no-connect"></i>
    </span>
  </div>
</template>
<script>
export default {
  name: "Vinput",
  props: {
    value: {},
    type: {
      type: String
    },
    maxlength: {
      type: Number,
      default: 6
    },
    minlength: {
      type: Number
    },
    showWordLimit: {
      type: Boolean
    },
    placeholder: {
      type: String,
      default: "请输入内容"
    },
    clearable: {
      type: Boolean,
      default: true
    },
    showPassword: {
      type: Boolean
    },
    disabled: {
      type: Boolean,
      default: false
    },
    size: {
      type: String
    },
    prefixIcon: {
      type: String
    },
    suffixIcon: {
      type: String
    },
    rows: {
      type: Number
    },
    autosize: {},
    autocomplete: {
      type: String
    },
    name: {
      type: String
    },
    readonly: {
      type: Boolean
    },
    max: {},
    min: {},
    step: {},
    resize: {
      type: String
    },
    autofocus: {
      type: Boolean
    },
    form: {
      type: String
    },
    label: {
      type: String
    },
    tabindex: {
      type: String
    },
    validateEvent: {
      type: Boolean
    }
  },
  data() {
    return {
      isFocus: false,
      isClearable: false
    };
  },
  methods: {
    input: function() {
      this.$emit("input", event.target.value);
    },
    focus: function() {
      this.isFocus = true;
    },
    mouseenter: function() {
        if (this.value != '' && this.clearable) {
            this.isClearable = true;
        }
    },
    mouseleave: function() {
        if (!this.isFocus) {
            this.isClearable = false;
        }
    },

  },
  computed: {
      
  },
  mounted: function() {
    this.$nextTick(function() {
      this.isClearable = this.clearable && this.value != '' && this.isFocus
    });
  }
};
</script>
<style scoped lang="stylus">
.v-input {
  position: relative;
  display: inline-block;
  width: 180px;
  font-size: $fontSize;
  text-align: center;
}
input {
  display: inline-block;
  width: 100%;
  height: 40px;
  padding: 0 15px;
  color: $mainTextColor;
  background: #fff;
  line-height: 40px;
  outline: none;
  box-sizing: border-box;
  border-radius: 4px;
  border: 1px solid $mainBorderColor;
  cursor: pointer;
}
input:focus {
    border-color: $mainColor;
}
.clearable {
  position: absolute;
  width: 25px;
  height: 100%;
  line-height: 40px;
  top: 0;
  right: 5px;
  color: $disabledColor;
  cursor: pointer;
}
.clearable:hover {
  color: #909399;
}
.disabled {
    color: $disabledColor;
    background: #f5f7fa;
    cursor: not-allowed;
}
</style>