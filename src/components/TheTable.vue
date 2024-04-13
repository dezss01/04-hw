<template>
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
    <tr v-for="(item, key) in data" :key="key">
      <th scope="row">{{item.name}}</th>
      <td>{{ item.price }}</td>
      <td>
        <AppInput
            :count="item.count"
            :max-count="item.maxCount"
            :min-count="item.minCount"
            @plus-count="addCount(key)"
            @minus-count="removeCount(key)"
            v-model:count="item.count"
        />
      </td>
      <td>{{ computedTotal(i)}}</td>
    </tr>
    </tbody>
  </table>
</template>

<script setup>
import AppInput from "./AppInput.vue";
import { data } from "../data.js";
import {computed} from "vue";

function addCount(i) {
  if(data.value[i].count < data.value[i].maxCount) {
    data.value[i].count += 1;
  }
}
function removeCount(i) {
  if(data.value[i].count > data.value[i].minCount) {
    data.value[i].count -= 1;
  }
}

const computedTotal = computed((i) => {
  return data.value[i].count * data.value[i].price
})

</script>

<style scoped>

</style>