<template>
  <div class="header_container">
    <h3>{{ title }}</h3>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "购物车",
    };
  },
};
</script>

<style scoped>
  .header_container {
    position: fixed;
    width: 100%;
    top: 0;
    color: #fff;
    height: 40px;
    line-height: 40px;
    text-align: center;
    background-color: #1c7aff;
  }
</style>