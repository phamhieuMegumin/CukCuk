<template>
  <div>
    <div
      :class="[
        'field__input',
        inputIcon ? 'field__input--icon' : '',
        inputLabel ? 'field__input__lable' : '',
        validate ? 'field__input--danger' : '',
      ]"
    >
      <label v-if="inputLabel" :for="labelFor"
        >{{ labelContent }}
        <span v-if="required" class="label__required">*</span></label
      >
      <input
        :type="date ? 'date' : 'text'"
        :id="labelFor"
        name="search__input"
        :placeholder="placeholder"
        :value="setValue ? setValue : value"
        @input="handleChange"
        @blur="handleBlur"
        autocomplete="off"
      />
      <span class="validate" v-if="required && validate"
        >{{ labelContent }} không được để trống</span
      >
      <div v-if="inputIcon" class="search__icon"></div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      text: "",
      validate: null,
    };
  },
  props: [
    "inputIcon",
    "placeholder",
    "inputLabel",
    "labelFor",
    "labelContent",
    "date",
    "value", // truyền dữ liệu
    "setValue", // set lại giá trị cho input
    "required", // set option required
  ],
  methods: {
    handleChange: function(e) {
      this.$emit("input", e.target.value);
    },
    handleBlur(e) {
      if (e.target.value.length == 0 && this.required) {
        this.validate = true;
      } else this.validate = false;
    },
  },
};
</script>

<style scoped>
.field__input {
  position: relative;
}

.field__input input {
  border: 1px solid #bbb;
  border-radius: 4px;
  height: 40px;
  font-size: 13px;
  font-family: GoogleSans-Regular;
  color: #000;
  outline: none;
  padding: 0 16px;
}

.search__icon {
  position: absolute;
  width: 16px;
  height: 16px;
  background-image: url("../../assets/icon/search.png");
  background-size: contain;
  top: 50%;
  left: 16px;
  transform: translateY(-50%);
}
.field__input--icon input {
  padding-left: 40px;
}
.field__input input:focus {
  border-color: #019160;
}
.field__input input::placeholder {
  font-size: 11px;
}
.field__input--icon input::placeholder {
  font-size: 12px;
}
.field__input input:focus::placeholder {
  color: transparent;
}
.field__input__lable {
  margin-top: 10px;
}
.field__input__lable input {
  width: 100%;
}
.field__input__lable label {
  font-size: 13px;
  font-family: GoogleSans-Medium;
  margin-bottom: 4px;
  display: block;
}
input[type="date"] {
  width: 100%;
}
.label__required {
  color: red;
}
.validate {
  position: absolute;
  top: 0;
  right: 0;
  color: red;
  display: block;
}
.field__input--danger input {
  border-color: red;
}
</style>
