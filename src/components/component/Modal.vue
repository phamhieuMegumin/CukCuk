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
                        :labelFor="'EmployeeCode(*)'"
                        v-model="employee.EmployeeCode"
                      />
                      <Input
                        :inputLabel="true"
                        :labelContent="'Ngày sinh'"
                        :labelFor="'DateOfBirth'"
                        :date="true"
                        v-model="employee.DateOfBirth"
                      />
                      <Input
                        :inputLabel="true"
                        :labelContent="'Số CMTND/Căn cước(*)'"
                        :labelFor="'IdentityNumber'"
                        v-model="employee.IdentityNumber"
                      />
                      <Input
                        :inputLabel="true"
                        :labelContent="'Nơi cấp'"
                        :labelFor="'IdentityPlace'"
                        v-model="employee.IdentityPlace"
                      />
                      <Input
                        :inputLabel="true"
                        :labelContent="'Email(*)'"
                        :labelFor="'Email'"
                        :placeholder="'example@domain.com'"
                        v-model="employee.Email"
                      />
                    </div>
                    <div class="modal__input--left">
                      <Input
                        :inputLabel="true"
                        :labelContent="'Họ và tên(*)'"
                        :labelFor="'FullName'"
                        v-model="employee.FullName"
                      />
                      <Dropdown
                        :optionValue="['0', '1', null]"
                        :optionText="['Nữ', 'Nam', 'Khác']"
                        :labelFor="'Giới tính'"
                        :dropName="'Gender'"
                        @getValue="handleGetValue"
                        :value="employee.Gender"
                      />
                      <Input
                        :inputLabel="true"
                        :labelContent="'Ngày cấp'"
                        :labelFor="'IdentityDate'"
                        :date="true"
                        v-model="employee.IdentityDate"
                      />
                      <div class="line"></div>
                      <Input
                        :inputLabel="true"
                        :labelContent="'Số điện thoại(*)'"
                        :labelFor="'PhoneNumber'"
                        v-model="employee.PhoneNumber"
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
                        :optionValue="[
                          '3700cc49-55b5-69ea-4929-a2925c0f334d',
                          '25c6c36e-1668-7d10-6e09-bf1378b8dc91',
                          '148ed882-32b8-218e-9c20-39c2f00615e8',
                        ]"
                        :optionText="[
                          'Giám đốc',
                          'Thu ngân',
                          'Nhân viên Marketing',
                        ]"
                        :labelFor="'Vị trí'"
                        :dropName="'PositionId'"
                        @getValue="handleGetValue"
                        :value="employee.PositionId"
                      />
                      <Input
                        :inputLabel="true"
                        :labelContent="'Mã số thuế cá nhân'"
                        :labelFor="'PersonalTaxCode'"
                        v-model="employee.PersonalTaxCode"
                      />
                      <Input
                        :inputLabel="true"
                        :labelContent="'Ngày gia nhập công ty'"
                        :labelFor="'JoinDate'"
                        v-model="employee.JoinDate"
                        :date="true"
                      />
                    </div>
                    <div class="modal__input--left">
                      <Dropdown
                        :optionValue="[
                          '142cb08f-7c31-21fa-8e90-67245e8b283e',
                          '469b3ece-744a-45d5-957d-e8c757976496',
                          '17120d02-6ab5-3e43-18cb-66948daf6128',
                          '4e272fc4-7875-78d6-7d32-6a1673ffca7c',
                        ]"
                        :optionText="[
                          'Phòng Marketting',
                          'Phòng Nhân sự',
                          'Phòng Đào tạo',
                          'Phòng Công nghệ',
                        ]"
                        :labelFor="'Phòng ban'"
                        :dropName="'DepartmentId'"
                        @getValue="handleGetValue"
                        :value="employee.DepartmentId"
                      />
                      <Input
                        :inputLabel="true"
                        :labelContent="'Mức lương cơ bản'"
                        :labelFor="'Salary'"
                        v-model="employee.Salary"
                        :setValue="formatMoney"
                      />
                      <Dropdown
                        :optionValue="['1', '2']"
                        :optionText="['Đang làm việc', 'Đang thử việc']"
                        :labelFor="'Tình trạng công việc'"
                        :dropName="'WorkStatus'"
                        @getValue="handleGetValue"
                        :value="employee.WorkStatus"
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
        <!-- Delete modal -->
        <div v-if="deleteModal" class="delete__modal modal__content">
          <div class="delete__content">
            <div class="popup__title">Xóa nhân viên</div>
            <h1>
              Bạn có chắc muốn xóa nhân viên có mã
              {{ deleteEmployee.employeeCode }} hay không?
            </h1>
          </div>
          <div class="modal__content__bottom">
            <div class="btn__bottom__group">
              <div class="btn__cancel" @click="closeModal">
                Hủy
              </div>
              <div @click="handleDeleteEmployee">
                <Button :content="'Xóa'" :btnDelete="true" />
              </div>
            </div>
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
import axios from "axios";
import { v4 as uuidv4 } from "uuid";
export default {
  data() {
    return {
      employee: {
        EmployeeId: uuidv4(),
        EmployeeCode: "",
        FirstName: null,
        LastName: null,
        FullName: "",
        Gender: null,
        DateOfBirth: null,
        PhoneNumber: "",
        Email: "",
        Address: null,
        IdentityNumber: "",
        IdentityDate: null,
        IdentityPlace: "",
        JoinDate: null,
        MaritalStatus: 0,
        PersonalTaxCode: "",
        Salary: null,
        EducationalBackground: 0,
        WorkStatus: 1,
        PositionId: null,
        PositionName: null,
        DepartmentId: null,
        DepartmentName: null,
        QualificationId: null,
        QualificationName: null,
        GenderName: "Nam",
        WorkStatusName: "Đang làm việc",
        MISAEntityState: 0,
      },

      // money
      formatMoney: "",
      url: "http://api.manhnv.net/v1/Employees",
      method: "post",
    };
  },
  props: [
    "customerModal",
    "deleteModal",
    "showModal",
    "setValue",
    "deleteEmployee",
  ],
  computed: {
    fomatMoney() {
      let currentValue = this.employee.Salary;
      currentValue = currentValue.replaceAll(".", "");
      if (this.employee.Salary.length > 3) {
        const money = currentValue.replace(/\B(?=(\d{3})+(?!\d))/g, ".");
        return money;
      }
      return currentValue;
    },
  },
  watch: {
    "employee.Salary": function() {
      this.formatMoney = this.fomatMoney;
    },
    setValue() {
      this.employee = { ...this.setValue };
      this.url = `http://api.manhnv.net/v1/Employees/${this.employee.EmployeeId}`;
      this.method = "put";
    },
  },
  components: { Button, Input, Dropdown },

  methods: {
    closeModal: function() {
      this.$emit("handleCloseModal");
    },
    handleGetValue: function(value, name) {
      if (name == "Gender") this.employee.Gender = parseInt(value);
      if (name == "PositionId") this.employee.PositionId = value;
      if (name == "WorkStatus") this.employee.WorkStatus = parseInt(value);
      if (name == "DepartmentId") this.employee.DepartmentId = value;
    },
    onSave: async function() {
      try {
        await axios({
          method: this.method,
          url: this.url,
          data: this.employee,
        });
        (this.url = "http://api.manhnv.net/v1/Employees"), //reset url
          (this.method = "post"), // reset method
          this.closeModal();
        this.$emit("isRender"); // require reRender
        alert("them thanh cong");
      } catch (error) {
        console.log(error);
      }
    },
    async handleDeleteEmployee() {
      try {
        await axios({
          method: "delete",
          url: `http://api.manhnv.net/v1/Employees/${this.deleteEmployee.employeeId}`,
        });
        this.$emit("isRender");
        this.closeModal();
        alert("Xoa thanh cong");
      } catch (error) {
        console.log(error);
      }
    },
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
.delete__modal {
  width: 400px;
  height: 180px;
  position: relative;
}
.delete__content {
  padding: 24px;
}
.popup__title {
  font-size: 15px;
  font-weight: bold;
  margin-bottom: 10px;
}
.delete__modal .modal__content__bottom {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
}
</style>
