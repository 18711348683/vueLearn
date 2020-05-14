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
    <span v-if="isClearable" class="clearable"></span>
    <span></span>
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
      type: String
    },
    clearable: {
      type: Boolean
    },
    showPassword: {
      type: Boolean
    },
    disabled: {
      type: Boolean,
      default: true
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
      isFocus: false
    };
  },
  methods: {
    input: function() {
      this.$emit("input", this.value);
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
      isClearable: function() {
          return this.clearable && this.value != '' && this.isFocus;
      }
  }
};
</script>
<style scoped>
.v-input {
  width: 180px;
  font-size: 14px;
}
input {
  display: inline-block;
  width: 100%;
  height: 40px;
  padding: 0 15px;
  color: #606266;
  background: #fff;
  line-height: 40px;
  outline: none;
  border-radius: 4px;
  border: 1px solid #dcdfe6;
  cursor: pointer;
}
input:focus {
    border-color: #409eff;
}
.disabled {
    color: #c0c4cc;
    background: #f5f7fa;
    cursor: not-allowed;
}
</style>