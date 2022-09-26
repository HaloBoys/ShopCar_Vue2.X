<template>
  <div class="mygoods_container">
    <span class="goods_check">
      <input
        type="checkbox"
        name=""
        id=""
        :checked="goods_state"
        @change="checkChange($event, goods_id)"
      />
    </span>
    <img :src="goods_img" alt="" class="goods_img" />
    <div class="goods_main">
      <h5 class="goods_title">
        {{ goods_name }}
      </h5>
      <div class="goods_mod">
        <span class="goods_price"> ￥ {{ goods_price }}</span>
        <MyCount :goods_id="goods_id" :goods_count="goods_count"></MyCount>
      </div>
    </div>
  </div>
</template>

<script>
import MyCount from "./MyCount.vue";
export default {
  props: [
    "goods_id",
    "goods_state",
    "goods_img",
    "goods_name",
    "goods_price",
    "goods_count",
  ],
  data() {
    return {};
  },
  methods: {
    checkChange(e, id) {
      this.$emit("get-check", e.target.checked, id);
    },
  },
  components: {
    MyCount,
  },
};
</script>

<style scoped>
.mygoods_container {
  padding: 10px;
  display: flex;
  justify-content: flex-start;
  height: 100px;
  border-bottom: 1px solid #ccc;
}
.goods_check input {
  margin-right: 15px;
  margin-top: 45px;
}
.goods_img {
  margin-right: 15px;
}
.goods_main {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
.goods_mod {
  display: flex;
  justify-content: space-between;
}
.goods_price {
  font-weight: 700;
  color: red;
}
</style>