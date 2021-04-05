<template>
  <div class="list__customer">
    <div class="table__container">
      <table class="table">
        <thead>
          <tr>
            <th>Mã nhân viên</th>
            <th>Họ và tên</th>
            <th>Giới tính</th>
            <th>Ngày sinh</th>
            <th>Điện thoại</th>
            <th>Email</th>
            <th>Chức vụ</th>
            <th>Phòng ban</th>
            <th>Mức lương cơ bản</th>
            <th>Tình trạng công việc</th>
          </tr>
        </thead>
        <tbody>
          <Modal
            :customerModal="true"
            :showModal="showModal"
            @handleCloseModal="changeShowModal"
            :setValue="employeesInfo"
            @isRender="isRender"
          />
          <Modal
            :showModal="showDeleteModal"
            @handleCloseModal="changeShowDeleteModal"
            :deleteModal="true"
            :deleteEmployee="deleteEmployee"
            @isRender="isRender"
          />
          <EmployeeItem
            v-for="(item, index) in employees"
            :key="index"
            :employee="item"
            @handleShowModal="changeShowModal"
            @getDeleteId="getDeleteId"
            @getInfo="getInfo"
            :active="isSelected"
          />
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import EmployeeItem from "./EmployeeItem.vue";
import Modal from "../component/Modal";
import axios from "axios";
export default {
  props: ["addModal", "deleMode", "filter"],
  components: {
    EmployeeItem,
    Modal,
  },
  created() {
    this.getData();
  },

  data() {
    return {
      employees: null,
      employeesFilter: null,
      showModal: false,
      showDeleteModal: false,
      employeeCodeMax: null,
      employeesInfo: null,
      deleteEmployee: null,
      isSelected: null,
    };
  },
  watch: {
    addModal() {
      this.changeShowModal();
    },
    deleMode() {
      this.handleDeleteModal();
    },
    filter() {
      this.employees = [...this.employeesFilter];

      this.employees = this.handleFilter;
    },
  },

  computed: {
    handleFilter() {
      if (this.filter != "0")
        return this.employees.filter((item) => item.PositionId == this.filter);
      else return this.employees;
    },
  },

  methods: {
    async getData() {
      const data = await axios.get("http://api.manhnv.net/v1/Employees");
      this.employees = data.data;
      this.employeesFilter = data.data;
    },
    changeShowModal: function() {
      this.showModal = !this.showModal;
    },
    changeShowDeleteModal: function() {
      this.showDeleteModal = !this.showDeleteModal;
    },
    handleDeleteModal: function() {
      this.showDeleteModal = !this.showDeleteModal;
    },
    getDeleteId(employeeId, employeeCode) {
      console.log(employeeId, employeeCode);
      this.isSelected = employeeId;
      this.deleteEmployee = {
        employeeId,
        employeeCode,
      };
    },
    isRender() {
      this.getData();
    },
    async getInfo(employeeId) {
      try {
        const data = await axios.get(
          `http://api.manhnv.net/v1/Employees/${employeeId}`
        );
        this.employeesInfo = data.data;
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>

<style>
/* Table */
.list__customer {
  position: relative;
}
.table__container {
  position: absolute;
  top: 16px;
  bottom: 60px;
  height: 430px;
  overflow-y: auto;
}
.table {
  position: relative;
  width: 100%;
  text-align: left;
  border-collapse: collapse;
}

.table tr {
  height: 48px;
  transition: all linear 0.2s;
}
.table thead th {
  position: sticky;
  top: 0;
  background-color: #fff;
  box-shadow: 0 1px 1px -1px #bbb;
}

.table th,
.table td {
  padding-left: 5px;
  padding-right: 5px;
  border-bottom: 1px solid #dbdeff;
}
.table tr:hover {
  background-color: #dbdeff;
  cursor: pointer;
}
.table th:first-child,
.table td:first-child {
  padding-left: 16px;
}

.table th:last-child,
.table td:last-child {
  padding-right: 16px;
}
.table tr.active {
  background: #019160;
  color: #fff;
}
</style>
