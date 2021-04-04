<template>
  <tr
    @dblclick="
      getInfo(customer.CustomerId);
      handelShowModal();
    "
    @click="selectedItem"
    :class="[isActive ? 'active' : '']"
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
  data() {
    return {
      isActive: false,
    };
  },
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
    selectedItem: function() {
      this.isActive = !this.isActive;
    },
  },
};
</script>

<style scoped></style>
