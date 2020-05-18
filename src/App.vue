<template>
  <div id="app">
    <!-- radio
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
    ></Vradio> -->

    <!-- radioGroup
    <VradioGroup :value="radioGroup1">
      <VradioButton label="上海" v-on:input="radioGroup1 = $event"></VradioButton>
      <VradioButton label="北京" v-on:input="radioGroup1 = $event"></VradioButton>
      <VradioButton label="广州" v-on:input="radioGroup1 = $event"></VradioButton>
      <VradioButton label="深圳" v-on:input="radioGroup1 = $event"></VradioButton>
    </VradioGroup> -->

    <!-- checkbox  
    <Vcheckbox
      v-model="checkbox"
      label="备选项"
    ></Vcheckbox>  -->

    <!-- checkboxGroup checkbox
    <VcheckboxGroup v-model="checkedCities">
      <vcheckbox
        v-for="city in cities"
        :label="city"
        :title="city"
        :key="city"
        v-on:checked="changeCheckedCities($event)"
      ></vcheckbox>
    </VcheckboxGroup> -->

    <!-- checkboxGroup checkboxButton
    <VcheckboxGroup v-model="checkedButtonCitied">
      <VcheckboxButton
        v-for="city in cities"
        :label="city"
        :title="city"
        :key="city"
        v-on:checked="changeButtonCities($event)"
      ></VcheckboxButton>
    </VcheckboxGroup> -->

    <!-- checkboxGroup checkbox indeterminate
    <Vcheckbox
      v-model="checkboxAll"
      label="全选"
      :indeterminate="indeterminate"
      v-on:input="handleCheckAllChange($event)"
    ></Vcheckbox>

    <VcheckboxGroup v-model="checkedAllCities">
      <vcheckbox
        v-for="city in cities"
        :label="city"
        :title="city"
        :key="city"
        v-on:checked="handleCheckedCitiesChange($event)"
      ></vcheckbox>
    </VcheckboxGroup> -->

    <!-- checkboxGroup checkbox min max
    <VcheckboxGroup v-model="checkedCitiesMax" min=2 max=3>
      <vcheckbox
        v-for="city in cities"
        :label="city"
        :title="city"
        :key="city"
        v-on:checked="changeMaxCities($event)"
      ></vcheckbox>
    </VcheckboxGroup> -->

    <Vinput v-model="inputValue" maxlength="10" showWordLimit=true></Vinput>
    <!-- <Vinput v-model="inputValue" clearable=true></Vinput>
    <Vinput v-model="inputValue" showPassword=true></Vinput>
    <Vinput v-model="inputValue" suffixIcon="icon-table2"></Vinput>
    <Vinput v-model="inputValue" prefixIcon="icon-search"></Vinput>
    <Vinput v-model="inputValue" type="textarea" :autosize=4></Vinput> -->

  </div>
</template>

<script>
// import Vradio from "./components/v-radio.vue";
// import VradioGroup from "./components/v-radio-group.vue";
// import VradioButton from "./components/v-radio-button.vue";

// import Vcheckbox from "./components/v-checkbox.vue";
// import VcheckboxGroup from "./components/v-checkbox-group.vue";
// import VcheckboxButton from "./components/v-checkbox-button.vue";

import Vinput from './components/input.vue';

const cityOptions = ["上海", "北京", "广州", "深圳"];
export default {
  name: "App",
  data() {
    return {
      radioEn: "2",
      disabled: true,
      border: false,
      radioGroup1: "北京",
      checkbox: true,
      checkboxAll: false,
      indeterminate: true,
      cities: cityOptions,
      checkedCities: ["上海", "广州"],
      checkedAllCities: ["上海", "广州"],
      checkedButtonCitied: ["上海", "广州"],
      checkedCitiesMax: ["上海", "广州"],
      inputValue: ""
    };
  },
  components: {
    // Vradio,
    // VradioGroup,
    // VradioButton,
    // Vcheckbox,
    // VcheckboxGroup,
    // VcheckboxButton,
    Vinput
  },
  methods: {
    //处理checkbox选中的值
    changeCheckedCities: function(value) {
      this.checkedCities = value;
    },
    //处理indeterminate checkbox
    handleCheckedCitiesChange: function(value) {
      this.checkedAllCities = value;
      if (this.indeterminate) {
        if (this.checkedAllCities.length == this.cities.length) {
          this.checkboxAll = true;
          this.indeterminate = true;
        } else if (this.checkedAllCities.length == 0) {
          this.checkboxAll = false;
          this.indeterminate = false;
        } else {
          this.indeterminate = true;
          this.checkboxAll = false;
        }
      }
    },
    //处理indeterminate checkbox
    handleCheckAllChange: function(value) {
      let cities = ["上海", "北京", "广州", "深圳"];
      this.checkedAllCities = value ? cities : [];
      this.indeterminate = false;
    },
    //处理checkboxbutton的值
    changeButtonCities: function(value) {
      this.checkedButtonCitied = value;
    },
    //处理max min的事件
    changeMaxCities: function(value) {
      this.checkedCitiesMax = value;
    }
  }
};
</script>

<style lang="stylus">
.group-radio .button-radio:first-child .button-span {
  border-radius: 4px 0 0 4px;
  border-left: 1px solid $mainBorderColor;
}

.group-radio .button-radio:last-child .button-span {
  border-radius: 0 4px 4px 0;
}

.group-checkbox .button-checkbox:first-child .button-span {
  border-radius: 4px 0 0 4px;
  border-left: 1px solid $mainBorderColor;
}

.group-checkbox .button-checkbox:last-child .button-span {
  border-radius: 0 4px 4px 0;
}
</style>
