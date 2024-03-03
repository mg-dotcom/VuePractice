<script setup>
import { ref, computed, watch, watchEffect } from "vue";

// computed
const products = [
  {
    name: 'Apple MacBook Pro 17"',
    color: "Silver",
    category: "Laptop",
    price: 2999,
    id: "appleMacBookPro",
  },
  {
    name: "Microsoft Surface Pro",
    color: "White",
    category: "Laptop PC",
    price: 1999,
    id: "notebookSurfacePro",
  },
  {
    name: "Magic Mouse 2",
    color: "Black",
    category: "Accessories",
    price: 99,
    id: "mouseMagic2",
  },
];
const orderNums = {};
/* const orderNums = {
  appleMacBookPro: ref(0),
  notebookSurfacePro: ref(0),
  mouseMagic2: ref(0),
  // ... additional products
}; */
const totalEach = {};
/* const totalEach = {
  appleMacBookPro: computed(() => orderNums.appleMacBookPro.value * 2999),
  notebookSurfacePro: computed(() => orderNums.notebookSurfacePro.value * 1999),
  mouseMagic2: computed(() => orderNums.mouseMagic2.value * 99),
  // ... additional products
}; */
products.forEach((product) => {
  orderNums[product.id] = ref(0);
  totalEach[product.id] = computed(() => {
    return orderNums[product.id].value * product.price;
  });
});
const addToOrder = (productId) => {
  orderNums[productId].value++;
};
const total = computed(() => {
  return products.reduce((acc, product) => {
    return acc + totalEach[product.id].value;
  }, 0);
});
// --------------------------------

//watch
</script>

<template>
  <section class="computed m-5" v-show="true">
    <div class="computed">
      <h2 class="font-bold text-2xl pb-4">Computed</h2>
      <div class="text-xl pb-4 pl-2">Order App:</div>
      <table class="text-sm text-left text-gray-500">
        <thead class="text-xs text-gray-700 uppercase bg-gray-50">
          <tr>
            <th scope="col" class="px-6 py-3">Product name</th>
            <th scope="col" class="px-6 py-3">Color</th>
            <th scope="col" class="px-6 py-3">Category</th>
            <th scope="col" class="py-3">Price</th>
            <th scope="col" class="px-6 py-3"></th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="product in products"
            :key="product.id"
            class="bg-white border-b"
          >
            <th scope="row" class="px-6 py-4 font-medium text-gray-900">
              {{ product.name }}
            </th>
            <td class="px-6 py-4">{{ product.color }}</td>
            <td class="px-6 py-4">{{ product.category }}</td>
            <td class="py-4">${{ product.price }}</td>
            <td class="px-3">
              <img
                class="cursor-pointer"
                :id="product.id"
                @click="addToOrder(product.id)"
                src="./assets/plus.svg"
              />
            </td>
            <td class="py-4">
              {{ orderNums[product.id] }} {{ totalEach[product.id] }}
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    Total: {{ total }}
  </section>

  <section class="watch m-5">
    <h2 class="font-bold text-2xl pb-4">watch and watchEffect</h2>
  </section>
</template>

<style scoped></style>
