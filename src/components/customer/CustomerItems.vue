<template>
  <tr
    @dblclick="
      getInfo(customer.CustomerId);
      handelShowModal();
    "
  >
    <td>{{ customer.CustomerCode }}</td>
    <td>{{ customer.FullName }}</td>
    <td>{{ customer.GenderName }}</td>
    <td>{{ formatDDMMYYY }}</td>
    <td>{{ customer.CustomerGroupName }}</td>
    <td>{{ customer.PhoneNumber }}</td>
    <td>{{ customer.Email }}</td>
    <td>{{ customer.Address }}</td>
    <td></td>
  </tr>
</template>

<script>
export default {
  props: ["customer"],
  computed: {
    formatDDMMYYY: function() {
      const newday = new Date(this.customer.DateOfBirth);
      const strDay = newday.getDate();
      const strMonth = newday.getMonth();
      const strYear = newday.getFullYear();
      return `${strDay}/${strMonth}/${strYear}`;
    },
  },
  methods: {
    getInfo: function() {},
    handelShowModal: function() {
      this.$emit("handleShowModal");
    },
  },
};
</script>

<style scoped></style>
