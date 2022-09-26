<template>
  <div id="app">
    <MyHeader></MyHeader>
    <MyGoods
      v-for="item in carData"
      :key="item.id"
      :goods_id="item.id"
      :goods_state="item.goods_state"
      :goods_img="item.goods_img"
      :goods_name="item.goods_name"
      :goods_price="item.goods_price"
      :goods_count="item.goods_count"
      @get-check="getCheck"
    ></MyGoods>
    <MyFooter
      :isCheckedAll="isCheckedAll"
      :totalMoney="getTotalMoney"
      :totalCount="getTotalCount"
      @checkall_change="checkAllChange"
    ></MyFooter>
  </div>
</template>

<script>
import axios from "axios";
import MyHeader from "./components/MyHeader.vue";
import MyGoods from "./components/MyGoods.vue";
import MyFooter from "./components/MyFooter.vue";
export default {
  name: "App",
  components: {
    MyHeader,
    MyGoods,
    MyFooter,
  },
  data() {
    return {
      carData: [],
    };
  },
  computed: {
    isCheckedAll() {
      return this.carData.every((item) => item.goods_state === true);
    },
    getTotalMoney() {
      return this.carData
        .filter((item) => item.goods_state === true)
        .reduce((pre, item) => {
          return pre + item.goods_price * item.goods_count;
        }, 0);
    },
    getTotalCount() {
      return this.carData
        .filter((item) => item.goods_state === true)
        .reduce((pre, item) => {
          return pre + item.goods_count;
        }, 0);
    },
  },
  created() {
    this.initCarData();
  },
  mounted() {
    this.$bus.$on("count-change", this.countChange);
  },
  methods: {
    // 初始化购物车方法
    async initCarData() {
      const { data: res } = await axios.get("https://www.escook.cn/api/cart");
      if (res.status === 200) {
        this.carData = res.list;
        console.log(res.list);
      }
    },
    getCheck(checked, id) {
      this.carData.some((item) => {
        if (item.id == id) {
          item.goods_state = checked;
          return true;
        }
      });
    },
    // 接收 footer 组件全选状态
    checkAllChange(status) {
      this.carData.forEach((item) => {
        item.goods_state = status;
      });
    },
    countChange(data) {
      /* 
      1. 遍历 carData 找到指定 id 
      2. 将对应 id 的 count 赋值为传过来最新的值
      */
      this.carData.some((item) => {
        if (item.id == data.id) {
          item.goods_count = data.count;
          return true;
        }
      });
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
#app {
  position: relative;
  padding: 40px 0;
}
</style>
