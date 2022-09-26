# 准备工作

接口地址：https://www.escook.cn/api/cart

# 购物车案例

## MyGoods 复选框

数据通过 props 传递过来的，所以不要通过 v-model 双向绑定，这里使用自定义事件实现：

1.  mygoods 组件通过自定义事件将 checkbox 的状态和 id 传给 App
2.  App 接收，并将接收过来的数据修改给 data

## MyFooter 全选/反选

全选：

1. 定义计算属性，监听商品列表的状态（布尔值）
2. 将监听到的状态 传给子组件 MyFooter
3. 子组件 MyFooter 接收状态作为全选按钮的状态

## MyFooter 合计价格

1. 在 App 中通过计算属性计算出商品的总价。
```javascript
getTotalMoney() {
 return this.carData
   .filter((item) => item.goods_state === true)
   .reduce((pre, item) => {
     return pre + item.goods_price * item.goods_count;
   }, 0);
},
```
2. 通过 props 传递给 MyFooter 组件，渲染。
3. 保留两位小数点：`toFixed(2)`


反选：

1. 监听 MyFooter 全选 复选框 change 事件
2. 将监听到的值传递给 APP 组件
3. 在 APP 组件中遍历所有商品列表，赋予状态

## MyFooter 结算数量

实现思路：

在 App 组件中使用计算属性，计算出结算数量并使用 props 传递给 MyFooter 组件

## MyCount 组件

Count 数量初始化

1. 通过APP组件将 goods_count 传递给 MyGoods 组件，MyGoods 组件 再中转给 MyCount 组件。
2. MyCount 组件接收数据并渲染。

Count 商品加减操作

1. 监听 Count 组件按钮的事件，通过全局事件总线，将变化的状态传递给 APP（id 和 value）
2. APP 接收到状态，然后遍历 carData 数组，更新状态
```javascript
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
```

# Todo

-[ ] flex 快忘完了,布局道路举步维艰！