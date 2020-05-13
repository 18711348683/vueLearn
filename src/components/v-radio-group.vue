<template>
  <div class="group-radio" :value="value" :size="size" :disabled="disabled" :textColor="textColor">
    <slot></slot>
  </div>
</template>
<script>
//import bus from '../assets/event.js';
export default {
  name: "VradioGroup",
  props: {
    value: {},
    size: {
      type: String,
      default: "mini"
    },
    disabled: {
      type: Boolean,
      default: false
    },
    textColor: {
      type: String,
      default: "white"
    },
    fill: {
      type: String,
      default: "#409eff"
    }
  }
};
</script>
<style scoped>
</style>