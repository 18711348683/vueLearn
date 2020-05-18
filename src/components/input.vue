<template>
  <div class="v-input" @mouseenter="mouseenter" @mouseleave="mouseleave">
    <label class="label">{{ label }}</label>
    <textarea v-if="isTextarea" class="textarea" :rows="autosize" cols="50" :autofocus="autofocus"></textarea>

    <input
      v-if="!isTextarea"
      :type="isType"
      class="input"
      :class="[{'disabled': disabled}, {'prefix': prefix}, {'suffix': suffix}]"
      :value="value"
      :placeholder="placeholder"
      :disabled="disabled"
      :clearable="clearable"
      :autocomplete="autocomplete"
      :readonly="readonly"
      @input="input"
      @focus="focus"
      @blur="blur"
      :maxlength="maxlength"
    />

    <span v-if="isClearable && clearable" class="icon-common icon-suffix-common" @click="clear">
      <i class="icon-no-connect"></i>
    </span>

    <span v-if="isOpen && showPassword" class="icon-common icon-suffix-common" @click="changeType">
      <i class="icon-eye"></i>
    </span>

    <span v-if="suffix" class="icon-common icon-suffix-common">
      <i :class="[suffixIcon]"></i>
    </span>

    <span v-if="prefix" class="icon-common icon-prefix-common">
      <i :class="[prefixIcon]"></i>
    </span>

    <span v-if="showWordLimit" class="icon-common icon-suffix-common word-limit">
      <span>{{ valueLength }}/</span>
      <span>{{ maxlength }}</span>
    </span>

    <div>
      <ul>
        <li>三全鲜食（北新泾店）</li>
        <li>Hot honey 首尔炸鸡（仙霞路）</li>
        <li>新旺角茶餐厅</li>
        <li>泷千家(天山西路店)</li>
        <li>胖仙女纸杯蛋糕（上海凌空店）</li>
        <li>贡茶</li>
        <li>豪大大香鸡排超级奶爸</li>
        <li>茶芝兰（奶茶，手抓饼）</li>
        <li>十二泷町</li>
        <li>星移浓缩咖啡</li>
        <li>阿姨奶茶/豪大大</li>
        <li>新麦甜四季甜品炸鸡</li>
        <li>Monica摩托主题咖啡店</li>
        <li>浮生若茶（凌空soho店）</li>
        <li>NONO JUICE 鲜榨果汁</li>
        <li>CoCo都可(北新泾店）</li>
        <li>快乐柠檬（神州智慧店）</li>
        <li>Merci Paul cafe</li>
        <li>猫山王（西郊百联店）</li>
        <li>枪会山</li>
        <li>纵食</li>
        <li>钱记</li>
        <li>壹杯加</li>
        <li>唦哇嘀咖</li>
        <li>爱茜茜里(西郊百联)</li>
        <li>爱茜茜里(近铁广场)</li>
        <li>鲜果榨汁（金沙江路和美广店）</li>
        <li>开心丽果（缤谷店）</li>
        <li>超级鸡车（丰庄路店）</li>
        <li>妙生活果园（北新泾店）</li>
        <li>香宜度麻辣香锅</li>
        <li>凡仔汉堡（老真北路店）</li>
        <li>港式小铺</li>
        <li>蜀香源麻辣香锅（剑河路店）</li>
        <li>北京饺子馆</li>
        <li>饭典*新简餐（凌空SOHO店）</li>
        <li>焦耳·川式快餐（金钟路店）</li>
        <li>动力鸡车</li>
        <li>浏阳蒸菜</li>
        <li>四海游龙（天山西路店）</li>
        <li>樱花食堂（凌空店）</li>
        <li>壹分米客家传统调制米粉(天山店)</li>
        <li>福荣祥烧腊（平溪路店）</li>
        <li>速记黄焖鸡米饭</li>
        <li>红辣椒麻辣烫</li>
        <li>(小杨生煎)西郊百联餐厅</li>
        <li>阳阳麻辣烫</li>
        <li>南拳妈妈龙虾盖浇饭</li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  name: "Vinput",
  props: {
    value: {},
    type: {
      type: String,
      default: "text"
    },
    maxlength: {
      type: Number
    },
    minlength: {
      type: Number
    },
    showWordLimit: {
      type: Boolean
    },
    placeholder: {
      type: String,
      default: "请输入内容"
    },
    clearable: {
      type: Boolean,
      default: false
    },
    showPassword: {
      type: Boolean,
      default: false
    },
    disabled: {
      type: Boolean,
      default: false
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
      isFocus: false,
      isClearable: false,
      isOpen: false
    };
  },
  methods: {
    input: function() {
      let realValue = event.target.value;
      this.$emit("input", realValue);
      if (realValue != "") {
        this.isClearable = true;
      } else if (realValue == "") {
        this.isClearable = false;
      }
    },
    focus: function() {
      this.isFocus = true;
      this.isOpen = true;
    },
    blur: function() {
      this.isFocus = false;
      this.isClearable = false;
      if (this.value == "") {
        this.isOpen = false;
      }
    },
    mouseenter: function() {
      if (this.value != "") {
        this.isClearable = true;
      }
    },
    mouseleave: function() {
      if (!this.isFocus) {
        this.isClearable = false;
      }
    },
    clear: function() {
      this.$emit("input", "");
    },
    changeType: function() {
      if (this.isType == "text") {
        this.isType = "password";
      } else {
        this.isType = "text";
      }
    }
  },
  computed: {
    isType() {
      return this.type;
    },
    prefix() {
      if (this.prefixIcon != undefined) {
        return true;
      }
      return false;
    },
    suffix() {
      if (this.suffixIcon != undefined) {
        return true;
      }
      return this.clearable || this.showPassword;
    },
    isTextarea() {
      if (this.type == "textarea") {
        return true;
      }
      return false;
    },
    valueLength() {
      return this.value.length;
    }
  },
  mounted: function() {
    this.$nextTick(function() {});
  }
};
</script>
<style scoped lang="stylus">
.v-input {
  position: relative;
  display: inline-block;
  font-size: $fontSize;
}

.label {
  display: inline-block;
}

.input {
  display: inline-block;
  width: 180px;
  height: 40px;
  padding: 0 15px;
  color: $mainTextColor;
  background: #fff;
  line-height: 40px;
  outline: none;
  box-sizing: border-box;
  border-radius: 4px;
  border: 1px solid $mainBorderColor;
  cursor: pointer;
}

.textarea {
  display: inline-block;
  padding: 5px 15px;
  color: $mainTextColor;
  background: #fff;
  outline: none;
  box-sizing: border-box;
  border-radius: 4px;
  border: 1px solid $mainBorderColor;
  cursor: pointer;
}

.input:focus {
  border-color: $mainColor;
}

.icon-common {
  position: absolute;
  width: 25px;
  height: 100%;
  line-height: 40px;
  top: 0;
  color: $disabledColor;
  cursor: pointer;
  text-align: center;
}

.icon-suffix-common {
  right: 5px;
}

.icon-prefix-common {
  left: 5px;
}

.icon-common:hover {
  color: #909399;
}

.suffix {
  padding-right: 30px;
}

.prefix {
  padding-left: 30px;
}

.word-limit {
  width: 40px;
}

.disabled {
  color: $disabledColor;
  background: #f5f7fa;
  cursor: not-allowed;
}
</style>