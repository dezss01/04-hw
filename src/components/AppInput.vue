

<template>
  <button @click="removeCountByButton" class="btn btn-danger btn-sm">
    <FontAwesomeIcon :icon="faMinus" />
  </button>
  <input :value="count" @input="handleUpdateCount" type="text" class="mx-2" >
  <button @click="addCountByButton" class="btn btn-success btn-sm">
    <FontAwesomeIcon :icon="faSquarePlus" />
  </button>
  <button class="btn btn-danger btn-sm mx-2" @click="clearCount">
    <FontAwesomeIcon :icon="faTrash" />
  </button>
  <div class="mt-3">
    <div>Минимальное количество товаров: {{ props.minCount }}</div>
    <div>Максимальное количество товаров: {{ props.maxCount }}</div>
  </div>

</template>

<script setup>

import {FontAwesomeIcon} from "@fortawesome/vue-fontawesome";
import {faSquarePlus} from "@fortawesome/free-regular-svg-icons";
import {faMinus} from "@fortawesome/free-solid-svg-icons";
import {faTrash} from "@fortawesome/free-solid-svg-icons/faTrash";



const props = defineProps({
  count: { type: Number, required: true },
  minCount: { type: Number, required: true },
  maxCount: { type: Number, required: true },
})

const emit = defineEmits(['update:count'])

const handleUpdateCount = (event) => {
  let result = Number(event.target.value)
  if(result < props.minCount) {
    result = props.minCount
  } else if(result > props.maxCount) {
    result = props.maxCount
  } else if(Number.isNaN(result)) {
    result = props.minCount
  }
  emit('update:count', result)
}
const addCountByButton = () => {
  if(props.count === 0) {
    emit('update:count', props.minCount)
  } else if(props.count < props.maxCount) {
    emit('update:count', props.count += 1)
  }
}
const removeCountByButton = () => {
  if(props.count > props.minCount) {
    emit('update:count', props.count -= 1)
  }
}

const clearCount = () => {
  emit('update:count', 0)
}

</script>

<style scoped>

</style>