<template>
  <TheNav />
  <div class="container">
    <table class="table table-bordered mt-3">
      <thead>
      <tr>
        <th scope="col">Title</th>
        <th scope="col">Price</th>
        <th scope="col">Cnt</th>
        <th scope="col">Total</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="(product, key) in data" :key="key">
        <th scope="row">{{product.name}}</th>
        <td>{{ product.price }}</td>
        <td>
          <AppInput
              v-model:count="product.count"
              :max-count="product.maxCount"
              :min-count="product.minCount"
              @plus-count="addCountByButton(key)"
              @minus-count="removeCountByButton(key)"
          />
        </td>
        <td>{{ product.quantity }}</td>

      </tr>
      </tbody>
    </table>
    <h1 class="text-decoration-underline">Total: {{ productsTotalPrice }}</h1>
  </div>
</template>

<script setup>
import TheNav from "./components/TheNav.vue";
import AppInput from "./components/AppInput.vue";
import {data} from "./data.js";
import {computed} from "vue";


function addCountByButton(i) {
  if(data.value[i].count === 0) {
    data.value[i].count = data.value[i].minCount
  } else if(data.value[i].count < data.value[i].maxCount) {
    data.value[i].count += 1;
  }
}
function removeCountByButton(i) {
  if(data.value[i].count > data.value[i].minCount) {
    data.value[i].count -= 1;
  }
}


const productsTotalPrice = computed(() => {
  return Object.values(data.value).reduce((quantity, product) => quantity + (product.price * product.count), 0)
})



</script>