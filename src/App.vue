<script setup>
import { ref } from 'vue'

// 定義 menu 資料
const menu = ref([
  {
    id: 1,
    name: '珍珠奶茶',
    description: '香濃奶茶搭配QQ珍珠',
    price: 50,
    quantity: 20
  },
  {
    id: 2,
    name: '冬瓜檸檬',
    description: '清新冬瓜配上新鮮檸檬',
    price: 45,
    quantity: 18
  },
  {
    id: 3,
    name: '翡翠檸檬',
    description: '綠茶與檸檬的完美結合',
    price: 55,
    quantity: 34
  },
  {
    id: 4,
    name: '四季春茶',
    description: '香醇四季春茶，回甘無比',
    price: 45,
    quantity: 10
  },
  {
    id: 5,
    name: '阿薩姆奶茶',
    description: '阿薩姆紅茶搭配香醇鮮奶',
    price: 50,
    quantity: 25
  },
  {
    id: 6,
    name: '檸檬冰茶',
    description: '檸檬與冰茶的清新組合',
    price: 45,
    quantity: 20
  },
  {
    id: 7,
    name: '芒果綠茶',
    description: '芒果與綠茶的獨特風味',
    price: 55,
    quantity: 18
  },
  {
    id: 7,
    name: '抹茶拿鐵',
    description: '抹茶與鮮奶的絕配',
    price: 60,
    quantity: 20
  }
])

const tempData = ref({
  id: 0,
  name: '',
  description: '',
  price: 0,
  quantity: 0
})

function addQty(item) {
  item.quantity += 1
  console.log('click +1')
}

function minusQty(item) {
  if (item.quantity > 0) {
    item.quantity -= 1
    console.log('click -1')
  } else {
    item.quantity = 0
  }
}

function editItem(item) {
  tempData.value = { ...item }
  console.log('edit item', tempData.value)
}

function saveEdit() {
  const index = menu.value.findIndex((item) => item.id === tempData.value.id)
  menu.value[index] = { ...tempData.value }
  tempData.value = {
    id: 0,
    name: '',
    description: '',
    price: 0,
    quantity: 0
  }
}
</script>

<template>
  <div>
    <table>
      <thead>
        <tr>
          <th scope="col">品項</th>
          <th scope="col">描述</th>
          <th scope="col">價格</th>
          <th scope="col">庫存</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in menu" v-bind:key="item.id">
          <td>
            {{ item.name }}
          </td>
          <td>
            <small>{{ item.description }}</small>
          </td>
          <td>{{ item.price }}</td>
          <td class="qtyBtn">
            <button type="button" @click="minusQty(item)">-</button>{{ item.quantity }}
            <button type="button" @click="addQty(item)">+</button>
          </td>
          <td class="editBtn"><button @click="editItem(item)">編輯</button></td>
        </tr>
      </tbody>
    </table>
    <hr />
    <div class="editWrapper">
      <h2>更改商品資訊</h2>
      <div class="inputWrapper">
        <label for="name">名稱: {{ tempData.name }} </label>
        <input id="name" type="text" v-model="tempData.name" />
      </div>

      <div class="inputWrapper">
        <label for="description">商品描述: {{ tempData.description }} </label>
        <input id="description" type="text" v-model="tempData.description" />
      </div>

      <div class="inputWrapper">
        <label for="price">價錢: {{ tempData.price }} 元</label>
        <input id="price" type="text" v-model="tempData.price" />
      </div>

      <div class="inputWrapper">
        <label for="quantity">庫存: {{ tempData.quantity }} 個</label>
        <input id="quantity" type="text" v-model="tempData.quantity" />
      </div>
      <button @click="saveEdit">儲存編輯</button>
    </div>
  </div>
</template>

<style>
.qtyBtn {
  width: 100px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 5px;
}
.editWrapper {
  padding: 10px;
}
.inputWrapper {
  margin: 10px 0;
}
label {
  margin-right: 5px;
}
</style>
