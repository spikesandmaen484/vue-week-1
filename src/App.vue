<script setup>
import { ref } from 'vue';

//飲料品項
const drink_items = ref([
  {
    id: 1,
    name: '珍珠奶茶',
    description: '香濃奶茶搭配QQ珍珠',
    price: 50,
    qty: 20,
    isEdit: false
  },
  {
    id: 2,
    name: '冬瓜檸檬',
    description: '清新冬瓜配上新鮮檸檬',
    price: 45,
    qty: 18,
    isEdit: false
  },
  {
    id: 3,
    name: '翡翠檸檬',
    description: '綠茶與檸檬的完美結合',
    price: 55,
    qty: 34,
    isEdit: false
  },
  {
    id: 4,
    name: '四季春茶',
    description: '香醇四季春茶，回甘無比',
    price: 45,
    qty: 10,
    isEdit: false
  },
  {
    id: 5,
    name: '阿薩姆奶茶',
    description: '阿薩姆紅茶搭配香醇鮮奶',
    price: 50,
    qty: 25,
    isEdit: false
  },
  {
    id: 6,
    name: '檸檬冰茶',
    description: '檸檬與冰茶的清新組合',
    price: 45,
    qty: 20,
    isEdit: false
  },
  {
    id: 7,
    name: '芒果綠茶',
    description: '芒果與綠茶的獨特風味',
    price: 55,
    qty: 18,
    isEdit: false
  },
  {
    id: 8,
    name: '抹茶拿鐵',
    description: '抹茶與鮮奶的絕配',
    price: 60,
    qty: 20,
    isEdit: false
  }
]);

//暫存品項
const tempName = ref('');

//庫存+1
const stockAdd = (id) => {
  drink_items.value[id - 1].qty++;
}

//庫存-1
const stockDecrease = (id) => {
  drink_items.value[id - 1].qty--;
}

//點編輯品項
const editName = (id) => {
  const index = drink_items.value.findIndex(item => item.id === id);
  tempName.value = drink_items.value[index].name;
  drink_items.value[index].isEdit = true;
}

//點儲存
const saveName = (id) => {
  const index = drink_items.value.findIndex(item => item.id === id);
  drink_items.value[index].isEdit = false; 
}

//點取消
const cancelSave = (id) => {
  const index = drink_items.value.findIndex(item => item.id === id);
  drink_items.value[index].name = tempName.value;
  drink_items.value[index].isEdit = false;
}

</script>

<template>
  <header>
    <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Vue-餐點管理工具</title>
        <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet" 
        integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">
  </header>

  <body>
    <div class="container">
      <table class="table">
        <thead>
          <tr>
            <th scope="col">品項</th>
            <th scope="col">描述</th>
            <th scope="col">價格</th>
            <th scope="col">庫存</th>
            <th></th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="drink in drink_items" :key="drink.id">
            <td>{{ drink.name }}</td>
            <td><small>{{ drink.description }}</small></td>
            <td>{{ drink.price }}</td>
            <td>
              <button type="button" @click="stockDecrease(drink.id)" :disabled="drink.qty <= 0">-</button>
              {{ drink.qty }}
              <button type="button" @click="stockAdd(drink.id)">+</button>
            </td>
            <td v-if="drink.isEdit">
              <input type="text" v-model="drink.name"/>
              <button type="button" class="btn btn-primary" @click="saveName(drink.id)">儲存</button>
              <button type="button" class="btn btn-light" @click="cancelSave(drink.id)">取消</button>
            </td>
            <td v-else>
              <button type="button" class="btn btn-success" @click="editName(drink.id)">編輯品項</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </body>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
