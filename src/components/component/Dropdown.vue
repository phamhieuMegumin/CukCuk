<template>
  <div class="field__combobox">
    <lable v-if="labelFor">{{ labelFor }}</lable>
    <div class="combobox" @click="selectOption">
      <div class="text">
        {{ valueCurrent ? optionText[valueCurrent] : optionText[0] }}
      </div>
      <div class="drop__down__icon"></div>
    </div>
    <div v-if="isShowOption" class="combobox__option">
      <option
        v-for="(valueItem, index) in optionValue"
        :value="valueItem"
        :key="index"
        @click="changeValue"
        >{{ optionText[index] }}</option
      >
    </div>
  </div>
</template>

<script>
export default {
  props: ["optionValue", "optionText", "labelFor"],
  data() {
    return {
      valueCurrent: "",
      isShowOption: false,
    };
  },
  methods: {
    changeValue: function(e) {
      this.valueCurrent = e.target.value;
      this.selectOption();
    },
    selectOption: function() {
      this.isShowOption = !this.isShowOption;
    },
  },
};
</script>

<style scoped>
.field__combobox {
  margin-top: 10px;
  position: relative;
}
.combobox {
  height: 40px;
  width: 100%;
  border: 1px solid #bbbbbb;
  padding-left: 16px;
  padding-right: 16px;
  border-radius: 4px;
  outline: none;
  display: flex;
  justify-content: space-between;
  align-items: center;
  box-sizing: border-box;
  cursor: pointer;
}

.combobox:hover {
  border-color: #019160;
}
.drop__down__icon {
  background-image: url("../../assets/icon/btn-next-page.svg");
  width: 13px;
  height: 13px;
  background-size: contain;
  transform: rotate(90deg);
}
.combobox__option {
  position: absolute;
  left: 0;
  top: calc(100% + 1px);
  border: 1px solid #bbbbbb;
  border-radius: 4px;
  width: 100%;
  z-index: 9999;
  background-color: white;
}
.combobox__option > * {
  height: 40px;
  line-height: 40px;
  padding: 0 16px;
  cursor: pointer;
}
.combobox__option > *:hover {
  background: #e9ebee;
}
lable {
  font-size: 13px;
  font-family: GoogleSans-Medium;
  margin-bottom: 4px;
  display: block;
}
</style>
