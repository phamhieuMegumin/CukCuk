<template>
  <tr
    @dblclick="
      getInfo(employee.EmployeeId);
      handelShowModal();
    "
    @click="selectedItem(employee.EmployeeId, employee.EmployeeCode)"
    :class="[employee.EmployeeId == active ? 'active' : '']"
  >
    <td>{{ employee.EmployeeCode }}</td>
    <td>{{ employee.FullName }}</td>
    <td>{{ employee.GenderName }}</td>
    <td>{{ formatDDMMYYY }}</td>
    <td>{{ employee.PhoneNumber }}</td>
    <td>{{ employee.Email }}</td>
    <td>{{ employee.PositionName }}</td>
    <td>{{ employee.DepartmentName }}</td>
    <td>{{ employee.Salary }}</td>
    <td>{{ employee.WorkStatusName }}</td>
  </tr>
</template>

<script>
export default {
  props: ["employee", "active"],
  data() {
    return {
      // isActive: false,
    };
  },
  computed: {
    formatDDMMYYY: function() {
      const newday = new Date(this.employee.DateOfBirth);
      const strDay = newday.getDate();
      const strMonth = newday.getMonth();
      const strYear = newday.getFullYear();
      return `${strDay}/${strMonth}/${strYear}`;
    },
  },
  methods: {
    getInfo: function(employeeId) {
      this.$emit("getInfo", employeeId);
    },
    handelShowModal: function() {
      this.$emit("handleShowModal");
    },
    selectedItem: function(employeesId, employeeCode) {
      // this.isActive = !this.isActive;
      this.$emit("getDeleteId", employeesId, employeeCode);
    },
  },
};
</script>

<style scoped></style>
