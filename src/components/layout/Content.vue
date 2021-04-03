<template>
  <div>
    <div class="main__content">
      <div class="main__content__top">
        <div class="main__content__left">
          <span>Danh sách nhân viên</span>
          <Input
            :inputIcon="true"
            :placeholder="'Tìm kiếm theo Mã, Tên Khác'"
          />
        </div>
        <div class="main__content__right">
          <div @click="addModal">
            <Button :btnIcon="true" :content="'Thêm khách hàng'" />
          </div>
          <div class="main__content__right-btn">
            <Button :content="'Delete'" :btnDelete="true" />
            <div class="btn__refresh">
              <div class="refresh__icon"></div>
            </div>
          </div>
        </div>
      </div>
      <ListCustomer :addModal="showModal" />
    </div>
  </div>
</template>

<script>
import Button from "../component/Button.vue";
import Input from "../component/Input.vue";
import ListCustomer from "../customer/ListCustomer.vue";
export default {
  components: { Button, Input, ListCustomer },
  data() {
    return {
      showModal: true,
    };
  },
  methods: {
    addModal: function() {
      this.showModal = !this.showModal;
    },
  },
};
</script>

<style scoped>
.main__content {
  padding: 24px;
  position: relative;
}

.main__content__top {
  display: flex;
  justify-content: space-between;
}

.main__content__left {
  margin-top: 5px;
}

.main__content__left > span {
  font-family: GoogleSans-Bold;
  font-size: 20px;
  margin-bottom: 14px;
  display: block;
}
.main__content__right-btn {
  display: flex;
  margin-top: 5px;
}
.btn__refresh {
  height: 40px;
  width: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  border: 1px solid #dbdeff;
  border-radius: 4px;
  margin-left: auto;
}

.refresh__icon {
  width: 16px;
  height: 16px;
  background-image: url("../../assets/icon/refresh.png");
  background-size: contain;
  background-repeat: no-repeat;
}

.main__content__table {
  margin-top: 16px;
  overflow-y: auto;
  max-height: 380px;
}

.content__bottom {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-top: 10px;
  position: absolute;
  bottom: 0;
  left: 24px;
  right: 24px;
  height: 56px;
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

.modal__content__top {
  padding: 24px;
}

.modal__main__content-top {
  display: flex;
}

.modal__main__content-top > * {
  width: 33.333333%;
  max-width: 33.333333%;
}

.modal__title {
  font-size: 20px;
  text-transform: capitalize;
  word-spacing: 3px;
  margin-bottom: 10px;
}
.modal__user__img {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
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
.modal__input--middle {
  margin: 0 10px;
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
.modal__content__middle__left input {
  width: 100%;
}
.address__input input {
  width: 100%;
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
.cancel__bnt {
  cursor: pointer;
}
</style>
