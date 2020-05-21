<template>
  <div class="container" :class="[{ focusColor: isFocus || active }, [size]]">
    <label>{{ label }}</label>
    <span
      class="number-common decrease"
      :class="[{ active: deActive }, { disabled: minLimit || disabled }, [size], [controlsPosition]]"
      @mouseenter="deEnter"
      @mouseleave="deLeave"
      @click="deClick"
    >
      <i v-if="controlsPosition != 'right'" class="icon-minus"></i>
      <i v-if="controlsPosition == 'right'" class="icon-ctrl"></i>
    </span>
    <input
      type="text"
      class="input"
      :class="[{ disabled: disabled }, [size], {left: controlsPosition == 'right'}]"
      v-model="innerValue"
      @focus="focus"
      @blur="blur"
    />
    <span
      class="number-common increase"
      :class="[{ active: inActive }, { disabled: maxLimit || disabled }, [size], [controlsPosition]]"
      @mouseenter="inEnter"
      @mouseleave="inLeave"
      @click="inClick"
    >
      <i v-if="controlsPosition != 'right'" class="icon-plus"></i>
      <i v-if="controlsPosition == 'right'" class="icon-ctrl"></i>
    </span>
  </div>
</template>
<script>
export default {
  name: "VinputNumber",
  props: {
    value: {
      type: Number,
      default: 0
    },
    min: {
      type: Number
    },
    max: {
      type: Number
    },
    step: {
      type: Number,
      default: 1
    },
    stepStrictly: {
      type: Boolean,
      default: false
    },
    precision: {
      type: Number,
      default: 0
    },
    size: {
      type: String
    },
    disabled: {
      type: Boolean,
      default: false
    },
    controls: {
      type: Boolean,
      default: false
    },
    controlsPosition: {
      type: String
    },
    name: {
      type: String
    },
    label: {
      type: String
    },
    placeholder: {
      type: String
    }
  },
  model: {
    prop: "value",
    event: "input"
  },
  data() {
    return {
      isFocus: false,
      active: false,
      inActive: false,
      deActive: false
    };
  },
  methods: {
    focus: function() {
      this.isFocus = true;
    },
    blur: function() {
      this.isFocus = false;

      let newValue = this.financial(event.target.value);
      let min = this.financial(this.min);
      let max = this.financial(this.max);
      let flag = newValue % this.step;

      if (newValue < min) {
        this.$emit("input", min);
        return;
      } else if (newValue > max) {
        this.$emit("input", max);
        return;
      }

      if (this.stepStrictly) {
        if (flag == 0) {
          this.$emit("input", newValue);
          return;
        } else {
          this.$emit(
            "input",
            this.financial(
              this.financial(newValue, this.step, "up"),
              flag,
              "down"
            )
          );
          return;
        }
      }

      this.$emit("input", newValue);
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
    inClick: function() {
      let value = this.financial(this.value, this.step, "up");
      let max = this.financial(this.max);
      if (!this.maxLimit && !this.disabled) {
        if (value > max) {
          this.$emit("input", max);
        } else {
          this.$emit("input", value);
        }
      }
    },
    deClick: function() {
      let value = this.financial(this.value, this.step, "down");
      if (!this.minLimit && !this.disabled) {
        let min = this.financial(this.min);
        if (!this.minLimit && !this.disabled) {
          if (value > min) {
            this.$emit("input", min);
          } else {
            this.$emit("input", value);
          }
        }
      }
    },
    financial: function(a, b, type) {
      if (type == "up") {
        return Number.parseFloat(a + b).toFixed(this.precision) * 1;
      } else if (type == "down") {
        return Number.parseFloat(a - b).toFixed(this.precision) * 1;
      } else {
        if (a == "") {
          return "";
        } else if (isNaN(a)){
          return Number.parseFloat(this.value).toFixed(this.precision) * 1;
        } else {
          return Number.parseFloat(a).toFixed(this.precision) * 1;
        }
      }
    }
  },
  computed: {
    innerValue: {
      get() {
        return this.financial(this.value);
      },
      set(value) {
        this.$emit("input", this.financial(value));
      }
    },
    minLimit() {
      if (parseFloat(this.value) <= parseFloat(this.min)) {
        return true;
      }
      return false;
    },
    maxLimit() {
      if (parseFloat(this.value) >= parseFloat(this.max)) {
        return true;
      }
      return false;
    }
  }
};
</script>
<style scoped lang="stylus">
.container {
  position: relative;
  line-height: 38px;
  width: 180px;
  border: 1px solid #dcdfe6;
  border-radius: 4px;
  cursor: pointer;
}

.container:hover {
  border-color: #c0c4cc;
}

.container.focusColor {
  border-color: #409eff;
}

.small.container {
  width: 200px;
  line-height: 34px;
}

.mini.container {
  width: 130px;
  line-height: 30px;
}

.number-common {
  position: relative;
  display: inline-block;
  width: 40px;
  background: #f5f7fa;
  color: #606266;
  text-align: center;
  font-size: 12px;
}

.small.number-common {
  width: 36px;
}

.mini.number-common {
  width: 32px;
}

.decrease {
  border-radius: 4px 0 0 4px;
  border-right: 1px solid #dcdfe6;
}

.increase {
  border-radius: 0 4px 4px 0;
  border-left: 1px solid #dcdfe6;
}

.right {
  position: absolute;
  height: 20px;
  right: 0;
  border-radius: 0 4px 0 0;
  border: 0;
  border-left: 1px solid #dcdfe6;
}

.right.decrease {
  bottom: 0;
}

.right.increase {
  height: 19px;
  top: 0;
  border-bottom: 1px solid #dcdfe6;
}

.right .icon-ctrl {
  position: absolute;
  left: 15px;
  top: 7px;
}

.right.decrease .icon-ctrl {
  top: 2px;
  transform: rotateX(180deg);
}

.input {
  appearance: none;
  outline: none;
  width: 98px;
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

.left.input {
  width: 138px;
}

.small.input {
  line-height: 34px;
  width: 126px;
}

.mini.input {
  line-height: 30px;
  width: 64px;
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
