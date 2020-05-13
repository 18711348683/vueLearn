<template>
  <div
    :value="value"
    :size="size"
    :disabled="disabled"
    :min="min"
    :max="max"
    :textColor="textColor"
    :fill="fill"
  >
    <slot></slot>
  </div>
</template>
<script>
export default {
  name: "VcheckboxGroup",
  props: {
    value: {},
    size: {
      type: String,
      default: "medium"
    },
    disabled: {
      type: Boolean,
      default: false
    },
    min: {
      type: Number
    },
    max: {
      type: Number
    },
    textColor: {
      type: String
    },
    fill: {
      type: String
    }
  }
};
</script>
<style scoped>
</style>