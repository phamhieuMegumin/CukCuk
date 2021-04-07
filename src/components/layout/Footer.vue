<template>
  <div>
    <footer class="footer">
      <div class="current__customer">
        Hiển thị <span>01-20/123</span> nhân viên
      </div>
      <div class="pagination">
        <div class="pagination__item btn__first__page">
          <div class="paginaton__icon icon__first__page"></div>
        </div>
        <div class="pagination__item btn__prev__page">
          <div class="paginaton__icon icon__prev__page"></div>
        </div>
        <div class="pagination__item pagination__item__num">
          <span>1</span>
        </div>
        <div class="pagination__item pagination__item__num">
          <span>2</span>
        </div>
        <div class="pagination__item pagination__item__num">
          <span>3</span>
        </div>
        <div class="pagination__item pagination__item__num">
          <span>4</span>
        </div>
        <div class="pagination__item btn__next__page">
          <div class="paginaton__icon icon__next__page"></div>
        </div>
        <div class="pagination__item btn__last__page">
          <div class="paginaton__icon icon__last__page"></div>
        </div>
      </div>
      <div class="current__customer__perpage">
        <span>20</span> nhân viên/trang
      </div>
    </footer>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
.footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-top: 10px;
  position: absolute;
  bottom: 0;
  left: 24px;
  right: 24px;
  height: 56px;
  background: #fff;
  border-top: 1px solid #bbbbbb;
}

.pagination {
  display: flex;
}

.pagination__item {
  width: 35px;
  height: 35px;
  border-radius: 4px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}

.pagination__item + .pagination__item {
  margin-left: 14px;
}

.paginaton__icon {
  width: 20px;
  height: 20px;
  background-size: contain;
}

.pagination__item:hover {
  background: #019160;
  color: #fff;
}

.icon__first__page {
  background-image: url("../../assets/icon/btn-firstpage.svg");
}

.icon__next__page {
  background-image: url("../../assets/icon/btn-next-page.svg");
}

.icon__last__page {
  background-image: url("../../assets/icon/btn-lastpage.svg");
}

.icon__prev__page {
  background-image: url("../../assets/icon/btn-prev-page.svg");
}

.pagination__item__num {
  border-radius: 50%;
  border: 1px solid #dbdeff;
}

.current__customer > span,
.current__customer__perpage > span {
  font-family: GoogleSans-Bold;
}
</style>
