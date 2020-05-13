<template>
  <div id="app">
    <Vradio
      title="备选项"
      name="radio"
      label="1"
      v-model="radioEn"
      v-bind:disabled="disabled"
      v-bind:border="border"
      size="mini"
    ></Vradio>

    <Vradio
      title="备选项"
      name="radio"
      label="2"
      v-model="radioEn"
      v-bind:border="border"
      size="small"
    ></Vradio>

    <Vradio
      title="备选项"
      name="radio"
      label="3"
      v-model="radioEn"
      v-bind:border="border"
      size="medium"
    ></Vradio>

    <VradioGroup :value="radioGroup1">
      <VradioButton label="上海" v-on:input="radioGroup1 = $event"></VradioButton>
      <VradioButton label="北京" v-on:input="radioGroup1 = $event"></VradioButton>
      <VradioButton label="广州" v-on:input="radioGroup1 = $event"></VradioButton>
      <VradioButton label="深圳" v-on:input="radioGroup1 = $event"></VradioButton>
    </VradioGroup>

    <vcheckbox v-model="checkboxEn"></vcheckbox>

    <vcheckboxGroup v-model="checkedCities">
      <vcheckbox v-for="city in cities" :label="city" :title="city" :key="city"></vcheckbox>
    </vcheckboxGroup>
  </div>
</template>

<script>
import Vradio from "./components/v-radio.vue";
import VradioGroup from "./components/v-radio-group.vue";
import VradioButton from "./components/v-radio-button.vue";

import Vcheckbox from "./components/v-checkbox.vue";
export default {
  name: "App",
  data() {
    return {
      radioEn: "2",
      disabled: true,
      border: false,
      radioGroup1: "北京",
      checkboxEn: true,
      cities: ["上海","北京","广州","深圳"],
      checkedCities: ["上海","广州"]
    };
  },
  components: {
    Vradio,
    VradioGroup,
    VradioButton,
    Vcheckbox
  }
};
</script>

<style lang="stylus">

.button-radio:first-child .button-span{
  border-radius: 4px 0 0 4px;
  border-left: 1px solid $mainBorderColor;
}
.button-radio:last-child .button-span{
  border-radius: 0 4px 4px 0;
}
</style>
