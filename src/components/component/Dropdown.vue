<template>
  <div>
    <select name="" id="">
      <option value="0">Nam</option>
      <option value="1">Nữ</option>
      <option value="">Value 3</option>
    </select>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
select {
  height: 40px;
  width: 100%;
  border: 1px solid #bbbbbb;
  padding-left: 16px;
  padding-right: 16px;
  border-radius: 4px;
  outline: none;
  box-sizing: border-box;
}
option {
  height: 30px;
}
option:hover {
  background: #e9ebee;
}

select:hover {
  border-color: #019160;
}
</style>
