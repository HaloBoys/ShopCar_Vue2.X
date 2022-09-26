<template>
  <div class="mycount_container">
    <button @click="sub">-</button>
    <span class="count_number">{{ goods_count }}</span>
    <button @click="add">+</button>
  </div>
</template>

<script>
export default {
  props: ["goods_id", "goods_count"],
  data() {
    return {};
  },
  methods: {
    sub() {
      if (this.goods_count - 1 == 0) return;
      const count_info = { id: this.goods_id, count: this.goods_count - 1 };
      this.$bus.$emit("count-change", count_info);
    },
    add() {
      const count_info = { id: this.goods_id, count: this.goods_count + 1 };
      this.$bus.$emit("count-change", count_info);
    },
  },
};
</script>

<style scoped>
button {
  width: 20px;
  height: 20px;
  border-radius: 25%;
  border: 1px solid #ccc;
}
.count_number {
  padding: 0 10px;
}
</style>