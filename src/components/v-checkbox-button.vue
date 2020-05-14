<template>
  <label class="button-checkbox">
    <span
      class="button-span"
      :class="[{'isActive': isChecked}, {'disabled': disabled || data.disabled}, [data.size]]"
      :style="activeStyle"
    >{{ label }}</span>
    <input
      type="checkbox"
      :label="label"
      :name="name"
      :disabled="disabled"
      :trueLabel="trueLabel"
      :falseLabel="falseLabel"
      :checked="checked"
      @change="change"
    />
  </label>
</template>
<script>
export default {
  name: "VcheckboxButton",
  props: {
    label: {},
    trueLabel: {},
    falseLabel: {},
    disabled: {
      type: Boolean,
      default: false
    },
    name: {
      type: String,
      default: "checkbox"
    },
    checked: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      data: this.$parent
    };
  },
  methods: {
    change: function() {
      if (this.isChecked) {
        this.$emit("checked", this.label + "/not");
      } else {
        this.$emit("checked", this.label);
      }
      this.$emit("input", !this.isChecked);
    }
  },
  computed: {
    activeStyle: function() {
      if (this.isChecked) {
        return {
          backgroundColor: this.data.fill,
          color: this.data.textColor,
          borderColor: this.data.fill
        };
      }
      return "";
    },
    isChecked: function() {
      let value = this.data.value;
      for (let i = 0; i < value.length; i++) {
        if (value[i] == this.label) {
          return true;
        }
      }
      return false;
    }
  }
};
</script>
<style scoped lang="stylus">
.button-checkbox {
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