<template>
  <div class="shopping-cart">
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
        <tr v-for="(item, index) in cartItems" :key="item.id">
          <td>{{ item.name }}</td>
          <td>¥{{ item.price.toFixed(2) }}</td>
          <td>
            <button @click="decreaseCount(index)">-</button>
            {{ item.count }}
            <button @click="increaseCount(index)">+</button>
          </td>
          <td>¥{{ (item.price * item.count).toFixed(2) }}</td>
        </tr>
      </tbody>
      <tfoot>
        <tr>
          <td colspan="3" class="total-label">总计</td>
          <td colspan="2" class="total-value">¥{{ totalPrice.toFixed(2) }}</td>
        </tr>
      </tfoot>
    </table>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const userName = ref('苏尚海')

const cartItems = ref([
  { id: 1, name: '商品 A', price: 29.99, count: 1 },
  { id: 2, name: '商品 B', price: 9.88, count: 1 },
])

const increaseCount = (index) => {
  cartItems.value[index].count++
}

const decreaseCount = (index) => {
  if (cartItems.value[index].count > 1) {
    cartItems.value[index].count--
  } else {
    alert('本次练习中，数量不可小于0')
  }
}

const totalPrice = computed(() => {
  return cartItems.value.reduce((total, item) => total + item.price * item.count, 0)
})
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

tfoot td {
  font-weight: bold;
  border-top: 2px solid #333;
  border-bottom: none;
}

.total-label {
  text-align: right;
}

.total-value {
  text-align: left;
  color: #e44d26;
}

.empty-cart {
  text-align: center;
  color: #999;
  font-size: 1.2em;
  margin-top: 40px;
}
</style>