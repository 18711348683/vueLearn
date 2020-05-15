<template>
  <label
    class="form-label"
    :class="[
    {'disabled': disabled || data.disabled || isDisabled}, 
    {'border': border}, {[sizeName]: border}, 
    {'checked': value || groupValue}, 
    {'indeterminate': indeterminate && !value}]"
  >
    <span class="input-checkbox"></span>
    <input
      type="checkbox"
      :value="value"
      :name="name"
      @change="change"
      :disabled="disabled || data.disabled || isDisabled"
      :label="label"
      :checked="checked"
      :trueLabel="trueLabel"
      :falseLabel="falseLabel"
      :indeterminate="indeterminate"
    />
    {{ label }}
  </label>
</template>
<script>
export default {
  name: "Vcheckbox",
  props: {
    title: {},
    value: {},
    label: {},
    trueLabel: {},
    falseLabel: {},
    disabled: {
      type: Boolean,
      default: false
    },
    border: {
      type: Boolean,
      default: false
    },
    size: {
      type: String,
      default: "mini"
    },
    name: {
      type: String,
      default: "checkbox"
    },
    checked: {
      type: Boolean,
      default: false
    },
    indeterminate: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      data: ""
    };
  },
  methods: {
    change: function() {
      if (this.data) {
        let value = this.data.value;
        this.label.split("");
        if (this.groupValue) {
          var pos = value.indexOf(this.label);
          value.splice(pos, 1);
        } else {
          value.push(this.label);
        }
        this.$emit("checked", value);
      } else {
        this.$emit("input", !this.value);
      }
    }
  },
  computed: {
    groupValue: function() {
      if (this.data) {
        let value = this.data.value;
        for (let i = 0; i < value.length; i++) {
          if (value[i] == this.label) {
            return true;
          }
        }
      }
      return false;
    },
    sizeName: function() {
      if (this.data) {
        let size = this.data.size;
        if (size) {
          return size;
        }
      }
      return this.size;
    },
    isDisabled: function() {
      if (this.data) {
        let value = this.data.value;
        let min = this.data.min;
        let max = this.data.max;
        if (value.length == min) {
          if (this.groupValue) {
            return true;
          }
        } else if (value.length == max) {
          if (!this.groupValue) {
            return true;
          }
        }
      }
      return false;
    }
  },
  mounted: function() {
    this.$nextTick(function() {
      let parent = this.$parent;
      if (parent.$options._componentTag == "VcheckboxGroup") {
        this.data = parent;
      } else {
        this.data = false;
      }
    });
  }
};
</script>
<style scoped lang="stylus">
.form-label {
  position: relative;
  display: inline-block;
  margin-left: 20px;
  font-size: $fontSize;
  color: $mainTextColor;
  cursor: pointer;
}
input {
  position: absolute;
  top: 0;
  left: 0;
  opacity: 0;
}
.input-checkbox {
  position: relative;
  display: inline-block;
  width: 14px;
  height: 14px;
  background: $mainBackgroundColor;
  border: 1px solid $mainBorderColor;
  border-radius: 2px;
  vertical-align: middle;
  margin-top: -2px;
  margin-left: 10px;
  margin-right: 10px;
}
.input-checkbox:hover {
  border-color: $mainColor;
}
.form-label.border {
  padding: 9px 20px 9px 0;
  border-radius: 4px;
  border: 1px solid $mainBorderColor;
}
.form-label.small {
  padding: 9px 20px 9px 0;
}
.checked .input-checkbox {
  background: $mainColor;
  border-color: $mainColor;
}
.indeterminate .input-checkbox {
  background: $mainColor;
  border-color: $mainColor;
}
.indeterminate .input-checkbox::after {
  position: absolute;
  left: 4px;
  right: 0;
  width: 6px;
  height: 1px;
  top: 6px;
  content: "";
  background:  $mainBackgroundColor;
}
.checked {
  color: $mainColor;
}
.checked .input-checkbox::after {
  position: absolute;
  left: 5px;
  top: 2px;
  height: 7px;
  width: 3px;
  content: "";
  border: 1px solid $mainBackgroundColor;
  border-left: 0;
  border-top: 0;
  transform: rotate(45deg) scaleY(1);
}
.border.checked {
  border-color: $mainColor;
}
.small.form-label {
  padding: 7px 20px 7px 0;
}
.mini.form-label {
  padding: 5px 15px 5px 0;
  font-size: 12px;
}
.mini .input-checkbox {
  width: 12px;
  height: 12px;
}
.mini .input-checkbox::after {
  top: 1px;
  left: 4px;
}
.disabled {
  color: $disabledColor;
  cursor: not-allowed;
}
.disabled.border {
  border-color: $disabledBorderColor;
}
.disabled .input-checkbox {
  background: #f5f7fa;
  border: 1px solid #e4e7ed;
}
.disabled .input-checkbox::after {
  border-color: $disabledColor;
}

</style>