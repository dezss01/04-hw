

<template>
  <button
      @click="removeCountByButton"
      :disabled="disableMinusButton"
      class="btn btn-danger btn-sm"
  >
    <FontAwesomeIcon :icon="faMinus" />
  </button>
  <input
      :value="count"
      @change="handleUpdateCount"
      type="text"
      class="mx-2"
      @input="inputValueMax"
  >
  <button
      @click="addCountByButton"
      :disabled="disablePlusButton"
      class="btn btn-success btn-sm"
  >
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
import {computed} from "vue";



const props = defineProps({
  count: { type: Number, required: true },
  minCount: { type: Number, required: true },
  maxCount: { type: Number, required: true },
})

const emit = defineEmits(['update:count'])

const handleUpdateCount = (event) => {
  let result = Number(event.target.value)
  // if(result < props.minCount) {
  //   result = props.minCount
  // } else if(result > props.maxCount) {
  //   result = props.maxCount
  // } else if(Number.isNaN(result)) {
  //   result = props.minCount
  // }
  // emit('update:count', result)
  // ниже реализация от gpt
  if(Number.isNaN(result)) {
    result = props.minCount
  } else {
    result = Math.min(Math.max(result, props.minCount), props.maxCount)
  }
  emit('update:count', result)
}
const addCountByButton = () => {
  if(props.count === 0) {
    emit('update:count', props.minCount)
  } else if(props.count < props.maxCount) {
    emit('update:count', (props.count + 1))
  }
}
const removeCountByButton = () => {
  if(props.count > props.minCount) {
    emit('update:count', (props.count - 1))
  }
}
const clearCount = () => {
  emit('update:count', 0)
}
const disableMinusButton = computed(() => {
  return props.count <= props.minCount
})
const disablePlusButton = computed(() => {
  return props.count >= props.maxCount
})

const inputValueMax = (event) => {
  if(Number.isNaN(event.target.value)) {
    event.target.value = props.minCount
    console.log('inputValueMax 1 условие')
  } else if(event.target.value > props.maxCount) {
    event.target.value = props.maxCount
  }
}
</script>

<style scoped>

</style>