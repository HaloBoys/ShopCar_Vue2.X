<template>
  <div class="myfooter_container">
    <span class="footer_check">
      <input
        type="checkbox"
        name=""
        id=""
        :checked="isCheckedAll"
        @change="footerCheckChange"
      />
      全选
    </span>

    <span>
      合计
      <span class="footer_total_price">￥ {{ totalMoney.toFixed(2) }}</span>
    </span>
    <span class="settle"> 结算 ({{ totalCount }}) &nbsp;&nbsp;</span>
  </div>
</template>

<script>
export default {
  props: ["isCheckedAll", "totalMoney", "totalCount"],
  data() {
    return {};
  },
  methods: {
    footerCheckChange(e) {
      this.$emit("checkall_change", e.target.checked);
    },
  },
};
</script>

<style scoped>
.myfooter_container {
  position: fixed;
  width: 100%;
  bottom: 0;
  display: flex;
  justify-content: space-between;
  height: 40px;
  line-height: 40px;
  border: 1px solid #ccc;
  background-color: #fff;
}
.footer_check {
  margin: 0 10px;
}
.footer_total_price {
  font-weight: 700;
  color: red;
}
.settle {
  padding: 0 10px;
  font-weight: 700;
  background-color: #1c7aff;
}
</style>