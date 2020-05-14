<template>
  <label
    class="form-label"
    :class="[{'blue': value}, {'disabled': disabled || data.disabled}, {'border': border}, {[sizeName]: border || data.size}, {'checked': value || isChecked}]"
  >
    <span class="input-checkbox"></span>
    <input
      type="checkbox"
      :value="value"
      :name="name"
      @change="change"
      :label="label"
      :checked="checked"
      :trueLabel="trueLabel"
      :falseLabel="falseLabel"
    />
    {{ title }}
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
      if (this.value || this.groupValue) {
        this.$emit("checked", this.label + "/not");
      } else {
        this.$emit("checked", this.label);
      }
      this.$emit("input", !this.value);
    }
  },
  computed: {
    isChecked: function() {
      if (this.data != "") {
        let value = this.data.value;
        for (let i = 0; i < value.length; i++) {
          if (value[i] == this.label) {
            return true;
          }
        }
      }
      return false;
    },
    groupValue: function() {
      if (this.data != "") {
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
      if (this.data != "") {
        let size = this.data.size;
        if (size) {
          return size;
        }
      }
      return this.size;
    }
  },
  mounted: function() {
    this.$nextTick(function() {
      let parent = this.$parent;
      if (parent.$options._componentTag == "VcheckboxGroup") {
        this.data = parent;
      } else {
        this.data = "";
      }
    });
  }
};
</script>
<style scoped>
.form-label {
  position: relative;
  display: inline-block;
  margin-left: 20px;
  font-size: 14px;
  color: #606266;
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
  background: #fff;
  border: 1px solid #dcdfe6;
  border-radius: 2px;
  vertical-align: middle;
  margin-top: -2px;
  margin-left: 10px;
  margin-right: 10px;
}
.input-checkbox:hover {
  border-color: #409eff;
}
.form-label.border {
  padding: 9px 20px 9px 0;
  border-radius: 4px;
  border: 1px solid #dcdfe6;
}
.form-label.small {
  padding: 9px 20px 9px 0;
}
.checked .input-checkbox {
  background: #409eff;
  border-color: #409eff;
}
.checked .input-checkbox::after {
  position: absolute;
  left: 5px;
  top: 2px;
  height: 7px;
  width: 3px;
  content: "";
  border: 1px solid #fff;
  border-left: 0;
  border-top: 0;
  transform: rotate(45deg) scaleY(1);
}
.border.checked {
  border-color: #409eff;
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
.blue {
  color: #409eff;
}
.disabled {
  color: #c0c4cc;
  cursor: not-allowed;
}
.disabled.border {
  border-color: #ebeef5;
}
.disabled .input-checkbox {
  background: #f5f7fa;
  border: 1px solid #e4e7ed;
}
.disabled .input-checkbox::after {
  border-color: #c0c4cc;
}
</style>