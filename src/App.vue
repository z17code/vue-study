
```vue
<template>
  <div class="shopping-cart">
    <!-- TODO1：此处在界面上应该展示出你的名字，请在模型中声明响应式状态 -->
    <h2>{{ userName }}的购物车</h2>
    <table>
      <thead>
        <tr>
          <th>商品</th>
          <th>单价</th>
          <th>数量</th>
          <th>小计</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>{{ cartItem.name }}</td>
          <td>¥{{ cartItem.price.toFixed(2) }}</td>
          <td>
            <!-- TODO2：请补充减按钮的点击事件监听，要求声明方法实现 -->
            <button @click="decreaseCount">-</button>
            <!-- TODO3：此处在界面上应该展示出商品数量，请在模型中声明响应式状态，要求初始值为1 -->
            {{ itemCount }}
            <button @click="increaseCount">+</button>
          </td>
          <!-- TODO4：请使用JavaScript表达式实现计算商品小计总价 -->
          <td>¥{{ total }}</td>
        </tr>
      </tbody>
      <tfoot>
        <tr>
          <td colspan="3" class="total-label">总计</td>
          <td colspan="2" class="total-value">¥...</td>
        </tr>
      </tfoot>
    </table>
  </div>
</template>

<script setup>
// TODO5：请补充import语句
import { ref } from 'vue';
// TODO6：请补充相关响应式状态声明，关联TODO1和TODO3
const itemCount = ref(1);
const userName = ref('张三');
const total = ref(0.0);
const cartItem = ref(
  { id: 1, name: '商品 A', price: 29.99 }
);

total.value = cartItem.value.price * itemCount.value;
const increaseCount = () => {
  itemCount.value++;
  total.value = cartItem.value.price * itemCount.value;
};

// TODO7 请定义并实现decreaseCount方法，注意数量不可小于0. 关联TODO2
function decreaseCount() {
  if (itemCount.value > 0) {
    itemCount.value--;
  }
  total.value = cartItem.value.price * itemCount.value;
}
</script>

<style scoped>
.shopping-cart {
  max-width: 800px;
  margin: 20px auto;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
  font-family: Arial, sans-serif;
}

h2 {
  text-align: center;
  color: #333;
}

table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
}

th, td {
  padding: 12px;
  text-align: center;
  border-bottom: 1px solid #ddd;
}

th {
  background-color: #f2f2f2;
  font-weight: bold;
}

td button {
  margin: 0 5px;
  padding: 4px 8px;
  cursor: pointer;
  background-color: #f0f0f0;
  border: 1px solid #ccc;
  border-radius: 4px;
}

td button:hover {
  background-color: #e0e0e0;
}
</style>
```