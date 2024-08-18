
<template>
  <table>
    <thead>
      <tr>
        <th scope="col">品項</th>
        <th scope="col">描述</th>
        <th scope="col">價格</th>
        <th scope="col">庫存</th>
        <th scope="col">操作</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(item, index) in items" :key="index">
        <td v-if="!tempEditedItems[index].isEdited">{{ item.name }}</td>
        <td v-else>
          <input type="text" v-model="tempEditedItems[index].name">
          <button @click="save(index)">儲存</button>
          <button @click="cancel(index)">取消</button>
        </td>
        <td><small>{{ item.description }}</small></td>
        <td>{{ item.price }}</td>
        <td>
          <button @click="decreaseInventory(item)" :disabled="item.inventory==0"> - </button>
          {{ item.inventory }}
          <button @click="increaseInventory(item)"> + </button></td>
        <td><button @click="editItemName(item, index)">編輯</button></td>
      </tr>
    </tbody>
  </table>

</template>

<script setup>
import { ref } from 'vue';

// 品項
const items = ref([
  {
    name:'珍珠奶茶',
    description:'香濃奶茶搭配QQ珍珠',
    price:50,
    inventory:20
  },
  {
    name:'冬瓜檸檬',
    description:'清新冬瓜配上新鮮檸檬',
    price:45,
    inventory:18
  },
  {
    name:'翡翠檸檬',
    description:'綠茶與檸檬的完美結合',
    price:55,
    inventory:34
  },
  {
    name:'四季春茶',
    description:'香醇四季春茶，回甘無比',
    price:45,
    inventory:10
  },
  {
    name:'阿薩姆奶茶',
    description:'阿薩姆紅茶搭配香醇鮮奶',
    price:50,
    inventory:25
  },
  {
    name:'檸檬冰茶',
    description:'檸檬與冰茶的清新組合',
    price:45,
    inventory:20
  },
  {
    name:'芒果綠茶',
    description:'芒果與綠茶的獨特風味',
    price:55,
    inventory:18
  },
  {
    name: '抹茶拿鐵',
    description: '抹茶與鮮奶的絕配',
    price: 60,
    inventory: 20
  }
])
const tempEditedItems = ref([
  { isEdited: false },
  { isEdited: false },
  { isEdited: false },
  { isEdited: false },
  { isEdited: false },
  { isEdited: false },
  { isEdited: false },
  { isEdited: false }
])


const tempEditItem = ref({});

const increaseInventory = (item) => {
  item.inventory++;
}
const decreaseInventory = (item) => {
  if(item.inventory > 0) {
    item.inventory--;
  }
}

const editItemName = (item, index) => {
  tempEditedItems.value[index] = {...item}
  tempEditedItems.value[index].isEdited=true
}

const save = (index) => {
  items.value[index] = tempEditedItems.value[index]
  delete items.value[index].isEdited;

  tempEditedItems.value[index] = { isEdited: false };
}
const cancel = (index) => {
  tempEditedItems.value[index].isEdited = false;
}

</script>

<style scoped>

th, td {
  padding: 5px;
  border: 1px solid black;
}

</style>
