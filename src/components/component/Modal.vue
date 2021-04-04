<template>
  <div>
    <div :class="['add__modal', showModal ? 'active' : '']">
      <div class="modal__layout">
        <div v-if="customerModal" class="modal__content">
          <div class="modal__content__top">
            <h3 class="modal__title">Thông tin nhân viên</h3>
            <div class="modal__main__content-top">
              <div class="modal__user__img">
                <div class="modal__img__box"></div>
                <div class="img__choose__notify">
                  <p>Vui lòng chọn ảnh có định dạng</p>
                  <p>.jpg, .jpeg, .png, .gif</p>
                </div>
              </div>
              <div class="modal__main">
                <div class="modal__input-group">
                  <div class="modal__input-title">
                    <h3>A. THÔNG TIN CHUNG:</h3>
                    <div class="line_border"></div>
                  </div>
                  <div class="modal__input-top">
                    <div class="modal__input--middle">
                      <Input
                        :inputLabel="true"
                        :labelContent="'Mã nhân viên'"
                        :labelFor="'customerCode'"
                        v-model="employee.CustomerCode"
                        ref="customerCode"
                      />
                      <Input
                        :inputLabel="true"
                        :labelContent="'Ngày sinh'"
                        :labelFor="'customerBirthDay'"
                        :date="true"
                        v-model="employee.DateOfBirth"
                      />
                      <Input
                        :inputLabel="true"
                        :labelContent="'Số CMTND/Căn cước'"
                        :labelFor="'customerGroupId'"
                        v-model="employee.MemberCardCode"
                      />
                      <Input
                        :inputLabel="true"
                        :labelContent="'Nơi cấp'"
                        :labelFor="'customerGroupId'"
                        v-model="employee.MemberCardCode"
                      />
                      <Input
                        :inputLabel="true"
                        :labelContent="'Email'"
                        :labelFor="'customerEmail'"
                        :placeholder="'example@domain.com'"
                        v-model="employee.Email"
                      />
                    </div>
                    <div class="modal__input--left">
                      <Input
                        :inputLabel="true"
                        :labelContent="'Họ và tên'"
                        :labelFor="'customerName'"
                        v-model="employee.FullName"
                      />
                      <Dropdown
                        :optionValue="['0', '1', '2']"
                        :optionText="['Nam', 'Nữ', 'Khác']"
                        :labelFor="'Giới tính'"
                      />
                      <Input
                        :inputLabel="true"
                        :labelContent="'Ngày cấp'"
                        :labelFor="'customerBirthDay'"
                        :date="true"
                        v-model="employee.DateOfBirth"
                      />
                      <div class="line"></div>
                      <Input
                        :inputLabel="true"
                        :labelContent="'Số điện thoại'"
                        :labelFor="'customerGroupName'"
                        v-model="employee.CustomerGroupId"
                      />
                    </div>
                  </div>
                </div>
                <!--  -->
                <!-- Thong tin cong viec -->
                <!--  -->
                <div class="modal__input-group">
                  <div class="modal__input-title">
                    <h3>B. THÔNG TIN CÔNG VIỆC:</h3>
                    <div class="line_border"></div>
                  </div>
                  <div class="modal__input-top">
                    <div class="modal__input--middle">
                      <Dropdown
                        :optionValue="['0', '1', '2']"
                        :optionText="['Nam', 'Nữ', 'Khác']"
                        :labelFor="'Vị trí'"
                      />
                      <Input
                        :inputLabel="true"
                        :labelContent="'Mã số thuế cá nhân'"
                        :labelFor="'customerBirthDay'"
                        v-model="employee.DateOfBirth"
                      />
                      <Input
                        :inputLabel="true"
                        :labelContent="'Ngày gia nhập công ty'"
                        :labelFor="'customerBirthDay'"
                        v-model="employee.DateOfBirth"
                        :date="true"
                      />
                    </div>
                    <div class="modal__input--left">
                      <Dropdown
                        :optionValue="['0', '1', '2']"
                        :optionText="['Nam', 'Nữ', 'Không xác định']"
                        :labelFor="'Phòng ban'"
                      />
                      <Input
                        :inputLabel="true"
                        :labelContent="'Mức lương cơ bản'"
                        :labelFor="'customerGroupName'"
                        v-model="employee.CustomerGroupId"
                        :setValue="formatMoney"
                      />
                      <Dropdown
                        :optionValue="['0', '1', '2']"
                        :optionText="['Nam', 'Nữ', 'Không xác định']"
                        :labelFor="'Tình trạng công việc'"
                      />
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="modal__content__bottom">
            <div class="btn__bottom__group">
              <div class="btn__cancel" @click="closeModal">
                Hủy
              </div>
              <div @click="onSave"><Button :content="'Lưu'" /></div>
            </div>
          </div>
          <div class="x__icon" @click="closeModal"></div>
        </div>
        <div v-if="deleteModal" class="modal__content">
          <h1>Bạn có muốn xóa khách hàng này</h1>
          <div class="btn__delete__group">
            <div class="btn btn__delete">Delete</div>
            <div class="btn btn__cancel">Hủy</div>
          </div>
          <div class="x__icon" @click="closeModal"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Button from "./Button.vue";
import Dropdown from "./Dropdown.vue";
import Input from "./Input";
// import axios from "axios";
// import { v4 as uuidv4 } from "uuid";
export default {
  data() {
    return {
      employee: {
        CustomerCode: "",
        FullName: "",
        Gender: 1,
        Address: "",
        DateOfBirth: null,
        Email: "",
        PhoneNumber: "",
        CustomerGroupId: "",
        DebitAmount: null,
        MemberCardCode: "",
        CompanyName: "",
        CompanyTaxCode: "",
        IsStopFollow: false,
        CustomerGroupName: "",
        GenderName: "Nam",
        MISAEntityState: 0,
      },

      // money
      formatMoney: "",
    };
  },
  computed: {
    fomatMoney() {
      let currentValue = this.employee.CustomerGroupId;
      currentValue = currentValue.replaceAll(".", "");
      if (this.employee.CustomerGroupId.length > 3) {
        const money = currentValue.replace(/\B(?=(\d{3})+(?!\d))/g, ".");
        return money;
      }
      return currentValue;
    },
  },
  watch: {
    "employee.CustomerGroupId": function() {
      this.formatMoney = this.fomatMoney;
    },
  },
  components: { Button, Input, Dropdown },
  props: ["customerModal", "deleteModal", "showModal"],

  methods: {
    closeModal: function() {
      this.$emit("handleCloseModal");
    },
    onSave: function() {},
  },
};
</script>

<style scoped>
.add__modal {
  display: none;
}
.add__modal.active {
  display: block;
}
.modal__layout {
  position: fixed;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background: rgba(0, 0, 0, 0.3);
  z-index: 999;
}
.modal__content {
  width: 80%;
  height: 90%;
  background: #fff;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  border-radius: 4px;
  overflow-y: auto;
}
.modal__content__bottom {
  background: #e9ebee;
  height: 60px;
  border-bottom-left-radius: 4px;
  border-bottom-right-radius: 4px;
}
.x__icon {
  position: absolute;
  width: 20px;
  height: 20px;
  right: 16px;
  top: 16px;
  background-image: url("../../assets/icon/x.svg");
  background-size: contain;
  cursor: pointer;
}
.modal__content__top {
  padding: 24px;
}

.modal__main__content-top {
  display: flex;
}

.modal__user__img {
  width: 33.333333%;
  max-width: 33.333333%;
  display: flex;
  align-items: center;
  flex-direction: column;
  margin-top: 30px;
}
.modal__main {
  width: 100%;
  margin-left: 10px;
}
.modal__input-top {
  display: flex;
  justify-content: space-between;
}
.modal__input-top > * {
  width: 50%;
}
.modal__title {
  font-size: 20px;
  text-transform: capitalize;
  word-spacing: 3px;
  margin-bottom: 10px;
}
.modal__img__box {
  border: 1px solid #bbbbbb;
  border-radius: 50%;
  width: 180px;
  height: 180px;
  overflow: hidden;
  background-image: url("../../assets/img/default-avatar.jpg");
  background-size: contain;
  background-position: center;
}
.modal__input-title {
  margin-top: 20px;
}
.modal__input--middle {
  margin-right: 10px;
}
.field__input__lable {
  margin-bottom: 15px;
}
.img__choose__notify > p {
  text-align: center;
}
.img__choose__notify > p:nth-child(2) {
  font-family: GoogleSans-Bold;
}
.checkbox__list {
  display: flex;
  margin-top: 10px;
}
.checkbox__item {
  display: flex;
  align-items: center;
}
.checkbox__item + .checkbox__item {
  margin-left: 20px;
}
.checkbox__item > span {
  margin-left: 5px;
}
.modal__content__middle {
  display: flex;
}
.modal__content__middle__left {
  width: 66.6666667%;
  max-width: 66.6666667%;
  margin-right: 10px;
}

.btn__bottom__group {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  height: 100%;
  width: 100%;
}
.btn__bottom__group > * {
  margin-right: 30px;
}
.btn__cancel {
  cursor: pointer;
}
.line {
  margin-top: 81px;
}
.line_border {
  width: 80px;
  height: 5px;
  background: #019160;
  margin-top: 15px;
}
</style>
