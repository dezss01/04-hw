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
              v-model:max-count="product.maxCount"
              v-model:min-count="product.minCount"
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





const productsTotalPrice = computed(() => {
  return Object.values(data.value).reduce((quantity, product) => quantity + (product.price * product.count), 0)
})



</script>