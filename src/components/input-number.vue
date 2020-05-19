<template>
  <div
    class="container"
    :class="[{ hoverColor: hoverColor }, { focusColor: isFocus || active }]"
  >
    <label>{{ label }}</label>
    <span
      class="number-common decrease"
      :class="[{ active: deActive }, { disabled: minLimit || disabled }]"
      @mouseenter="deEnter"
      @mouseleave="deLeave"
      @click="deClick"
      >-</span
    >
    <input
      type="text"
      class="input"
      :class="[{ disabled: disabled }]"
      :value="value"
      @mouseenter="mouseenter"
      @mouseleave="mouseleave"
      @focus="focus"
      @blur="blur"
      @input="change"
    />
    <span
      class="number-common increase"
      :class="[{ active: inActive }, { disabled: maxLimit || disabled }]"
      @mouseenter="inEnter"
      @mouseleave="inLeave"
      @click="inClick"
      >+</span
    >
  </div>
</template>
<script>
export default {
  name: "VinputNumber",
  props: {
    value: {
      type: Number,
      default: 0,
    },
    min: {
      type: Number,
    },
    max: {
      type: Number,
    },
    step: {
      type: Number,
      default: 1,
    },
    stepStrictly: {
      type: Boolean,
      default: false,
    },
    precision: {
      type: Number,
    },
    size: {
      type: String,
    },
    disabled: {
      type: Boolean,
      default: false,
    },
    controls: {
      type: Boolean,
      default: false,
    },
    controlsPosition: {
      type: String,
    },
    name: {
      type: String,
    },
    label: {
      type: String,
    },
    placeholder: {
      type: String,
    },
  },
  data() {
    return {
      hoverColor: false,
      isFocus: false,
      active: false,
      inActive: false,
      deActive: false,
    };
  },
  methods: {
    mouseenter: function() {
      this.hoverColor = true;
    },
    mouseleave: function() {
      this.hoverColor = false;
    },
    focus: function() {
      this.isFocus = true;
    },
    blur: function() {
      this.isFocus = false;
    },
    inEnter: function() {
      if (!this.maxLimit) {
        this.inActive = true;
        this.active = true;
      }
    },
    inLeave: function() {
      this.inActive = false;
      this.active = false;
    },
    deEnter: function() {
      if (!this.minLimit) {
        this.deActive = true;
        this.active = true;
      }
    },
    deLeave: function() {
      this.deActive = false;
      this.active = false;
    },
    change: function() {
      let newValue = parseInt(event.target.value);
      if (isNaN(newValue)) {
        this.$emit("input", this.value);
      } else {
        if (newValue < parseInt(this.min)) {
          this.$emit("input", parseInt(this.min));
        } else if (newValue > parseInt(this.max)) {
          this.$emit("input", parseInt(this.max));
        } else {
            let flag = newValue % this.step;
          if (this.stepStrictly && flag == 0) {
            this.$emit("input", newValue);
          } else {
            this.$emit("input", newValue + this.step - flag);
          }
        }
      }
    },
    inClick: function() {
      if (!this.maxLimit && !this.disabled) {
        this.$emit("input", parseInt(this.value) + this.step);
      }
    },
    deClick: function() {
      if (!this.minLimit && !this.disabled) {
        this.$emit("input", parseInt(this.value) - this.step);
      }
    },
  },
  computed: {
    minLimit() {
      if (parseInt(this.value) <= parseInt(this.min)) {
        return true;
      }
      return false;
    },
    maxLimit() {
      if (parseInt(this.value) >= parseInt(this.max)) {
        return true;
      }
      return false;
    },
  },
};
</script>
<style scoped lang="stylus">
.container {
  line-height: 38px;
  width: 180px;
  border: 1px solid #dcdfe6;
  border-radius: 4px;
  cursor: pointer;
}

.number-common {
  display: inline-block;
  width: 40px;
  background: #f5f7fa;
  color: #606266;
  text-align: center;
}

.decrease {
  border-radius: 0 0 4px 4px;
  border-right: 1px solid #dcdfe6;
}

.increase {
  border-radius: 4px 4px 0 0;
  border-left: 1px solid #dcdfe6;
}

.input {
  appearance: none;
  outline: none;
  width: 98px;
  height: 38px;
  padding: 0;
  color: #606266;
  text-align: center;
  background: #fff;
  border: none;
  cursor: pointer;
  line-height: 38px;
  vertical-align: top;
  display: inline-block;
}

.hoverColor {
  border-color: #c0c4cc;
}

.focusColor {
  border-color: #409eff;
}

.active {
  color: #409eff;
}

.disabled {
  color: #c0c4cc;
  background: #f5f7fa;
  cursor: not-allowed;
}
</style>
